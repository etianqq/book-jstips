SASS系统一般指的是to B/C的企业级应用，管理后台等。如常见供应链系统，合同管理系统，HR系统等。
在SPA兴起之前，一般都是后台渲染（JSP），或者，后台渲染菜单和导航，内容区域嵌入`iframe`，然后前端同学负责具体页面开发。

直到Angular，React，Vue等前端统一解决方案，或组件化前端框架兴起之后，SPA应用大行其道。它最大的特点就是前端负责路由（当然，如果是BrowserRouter模式，需要后台配合），后端只负责数据输出。如此一来，前后端可以完全独立开发，部署，发布。

后面，我们基于React来聊聊在SASS系统开发最核心的几个模块。

### 1. 创建项目

利用类似`create-react-app` 脚手架工具创建一个React项目。

#### 扩展webpack配置
`create-react-app`将webpack配置脚本都“隐藏”起来，只有运行`eject`命令才能看到原始配置脚本。如果你不想做弹射操作，又想修改或者增加webpack配置，那么，可以用`react-app-rewired`。

* `npm install react-app-rewired`
* 修改package.json文件中的`scripts`属性。
```
 "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-app-rewired eject"
  }
```
* 根目录下添加`config-overrides.js`文件，然后添加你想修改的webpack配置内容，比如，支持别名，支持antd全局样式导入，支持scss预处理器。
```
const { injectBabelPlugin } = require('react-app-rewired');
const path = require('path');

module.exports = function override(config, env) {
    // 支持别名
    config.resolve.alias = {
        api: path.join(__dirname, 'src/util/api'),
        '@': path.resolve(__dirname, './src/')
    }
    // 支持antd全局样式导入
    let enhance_config = injectBabelPlugin(
        ['import', { libraryName: 'antd', libraryDirectory: 'es', style: 'css' }],
        config);
    // 支持scss预处理器 
    let loaderList = config.module.rules[2].oneOf;
    loaderList.splice(loaderList.length - 1, 0, {
        test: /\.scss$/,
        use: ["style-loader", "css-loader", "sass-loader"]
    });
    return enhance_config;
};
```
* 最后运行`npm start`即可以启动开发环境。

### 2. 目录结构

一般一个完整的前端项目可能包含下面几个部分：

1. `layouts/`: 存放布局级别的组件
2. `pages/`: 存放页面级别的组件
3. `components/`: 存放业务级别的 UI 组件
4. `hocs/`: 存放业务级别的高阶逻辑组件（看情况可与 `components/` 合并，但建议分开）
5. `redux/`: 数据管理，如初始化 redux store 等（如果不用redux，可不需要这个文件夹）
6. `utils/`: 存放通用的功能性函数
7. `styles/`: 存放全局的 CSS 样式、变量、mixins 等
8. `config/`: 配置信息，如路由配置，菜单配置等
9. `i18n/`: 存放应用国际化需要的多语言文件
10. `assets/`: 存放**全局**静态资源，如图标、图片等

如果是组件或者页面的静态资源（如图片），我更喜欢跟着组件同级存储，便于修改。
![](https://images.xiaozhuanlan.com/photo/2019/f9d12287fef1ef38df3beafca561484a.jpg)

### 3. 页面布局

页面布局和路由是强相关的，只有设计好页面布局，才能更合理的设计路由系统。

下图是一个典型的SASS系统页面：
![](https://images.xiaozhuanlan.com/photo/2019/3addf25565df6c80b884e91fa90c859f.jpg)

当然，还需要登录页和注册页，这两个页面不包含菜单的。
![](https://images.xiaozhuanlan.com/photo/2019/f8312fbd550d9c1804205895b0630ff5.jpg)
![](https://images.xiaozhuanlan.com/photo/2019/98f82e2776efeba20f39eeb5cf32b1ce.jpg)

所以，我们的页面分为两大类，带导航`BasicLayout`的和不带导航`UserLayout`。

先看`BasicLayout`，包含三个子组件，上导航，左菜单和内容区，源码如下：
```
import React from 'react';
import { Layout, PageHeader } from 'antd';
import MyMenu from './component/MyMenu';
import MyHeader from './component/MyHeader';
import logo from '@/components/images/ktlogo.png';
import { routesHeader } from '@/config/routesHeader';

const { Header, Content } = Layout;

export default (props) => {

    function getHeaderTitle() {
        return routesHeader[props.location.pathname] ? routesHeader[props.location.pathname].title : '';
    }

    function getHeaderSubTitle() {
        return routesHeader[props.location.pathname] ? routesHeader[props.location.pathname].subTitle : '';
    }

    const headerTitle = getHeaderTitle();
    const headerSubTitle = getHeaderSubTitle()

    return (
        <Layout style={{ minHeight: '100vh' }}>
            {/* 上导航，包括Logo，用户状态，消息提示和登出按钮 */}
            <Header className='header'>
                <div className='logo'>
                    <img src={logo} alt='kingtower' />
                </div>
                <MyHeader history={props.history} />
            </Header>
            <Layout>
                {/* 左侧菜单导航栏 */}
                <MyMenu />
                <Content style={{ position: 'relative' }}>
                    {/* 根据routesHeader配置文件设置页面Header信息 */}
                    {headerTitle && headerSubTitle &&
                        <PageHeader backIcon={props.match.params ? true : false}
                            title={headerTitle} subTitle={headerSubTitle} />}
                    {/* 页面具体内容 */}
                    {props.children}
                </Content>
            </Layout>
        </Layout>
    )
}
```
要注意，上导航拥有自己的状态值，比如显示用户信息，显示消息内容等。所以，我们应该将它独立抽象出来，而不要和page页面混合。
另外，每个page页面都有格式相同的header栏，这部分UI也应该由`BasicLayout`提供，而具体数据由配置文件提供（因为每个页面的header的固定文案，所以用配置文件比较适合）。

然后看看`UserLayout`，它就比较简单了。
```
import React from 'react';
import { Layout } from 'antd';
import './UserLayout.scss';

const { Footer } = Layout;

export default (props) => {

    return (
        <Layout className='userLayout'>
            <div className='header'>
                <span className='meta'>
                    <span className='title'>Kingtower</span>
                </span>
                <p className='desc'>让后台接口开发简单而友好</p>
            </div>
            {/* 可能是登录页，或者注册页 */}
            {props.children}
            <Footer className='footer'>Ant Design ©2019 Created by kingtower</Footer>
        </Layout>
    )
}
```
整个layouts文件目录如下：
![](https://images.xiaozhuanlan.com/photo/2019/73260f499d926ab00238211b7f8cb04b.jpg)

### 4. 配置文件

相关的配置文件有3个：

* 左侧菜单配置
```
export const asideMenuConfig = [
    {
        name: '接口',
        path: '/module',
        icon: 'api',
        key: 1
    },
    {
        name: '构建',
        path: '/builder',
        icon: 'branches',
        key: 2
    },
    {
        name: '积木',
        path: '/block',
        icon: 'appstore',
        key: 3
    }
]
```
* 具体路由配置。
利用`React.lazy`做异步加载，再配合webpack构建工具分包。
这里用到了嵌套路由，比如`/user`是路由到`UserLayout`组件，加载`UserLayout`组件的同时，再次匹配是否是`/user/login`或`/user/register`，然后在`UserLayout`组件内部再加载子组件`UserLogin`或者`UserRegister`。
```
import React from 'react';

import BasicLayout from '@/layouts/BasicLayout';
import UserLayout from '@/layouts/UserLayout';

const ModuleView = React.lazy(() => import('@/pages/module/ModuleView'));
const Builder = React.lazy(() => import('@/pages/builder/Builder'));
const Block = React.lazy(() => import('@/pages/block/Block'));
const UserLogin = React.lazy(() => import('@/pages/UserLogin'));
const UserRegister = React.lazy(() => import('@/pages/UserRegister'));
const NotFound = React.lazy(() => import('@/pages/NotFound'));

const routerConfig = [
    {
        path: '/user',
        component: UserLayout,
        children: [
            {
                path: '/login',
                component: UserLogin
            },
            {
                path: '/register',
                component: UserRegister,
            },
            {
                path: '/',
                redirect: '/user/login',
            },
            {
                component: NotFound,
            },
        ]
    },
    {
        path: '/',
        component: BasicLayout,
        children: [
            {
                path: '/module',
                component: ModuleView,
                isNeedAuth: true
            },
            {
                path: '/builder',
                component: Builder,
                isNeedAuth: true
            },
            {
                path: '/builder/:id',
                component: Builder,
                isNeedAuth: true
            },
            {
                path: '/block',
                component: Block,
                isNeedAuth: true
            },
            {
                path: '/',
                redirect: '/module',
            },
        ]
    }
];

export default routerConfig;
```
* 页面Header配置
```
export const routesHeader = {
    "/module": {
        title: "模块",
        subTitle: "UI API和任务计算"
    },
    "/builder": {
        title: "流程图",
        subTitle: "构建你的API"
    },
    "/block": {
        title: "积木",
        subTitle: "模块的基础"
    }
}
```

### 5. 利用react-router创建路由

react-router的介绍可以参考文章[React进阶篇（九）React Router](https://xiaozhuanlan.com/topic/2031975486)，这里不再累述。
重点是，如何利用自定义的配置文件创建嵌套路由？看源码：
```
import React, { Suspense } from 'react';
import path from 'path';
import { HashRouter as Router, Route, Switch, Redirect } from 'react-router-dom';
import PageLoading from '@/components/PageLoading';
import ErrorBoundary from '@/components/ErrorBoundary';
import routes from './config/routes';
import { auth } from '@/util/auth';

const RouteItem = (props) => {
    const { redirect, path: routePath, component, key, isNeedAuth } = props;

    const isAuth = auth.isAuth();
    if (redirect) {
        return (
            <Redirect
                exact
                key={key}
                from={routePath}
                to={redirect}
            />
        );
    }
    else if (!isNeedAuth || (isNeedAuth && isAuth)) {
        return <Route
            key={key}
            component={component}
            path={routePath}
        />;
    }
    else {
        return <Redirect
            key={key}
            to={{
                pathname: '/user/login',
                state: { from: routePath }
            }}
        />
    }

};


export default () => {

    return (
        <Router>
            <Switch>
                {
                    routes.map((route, id) => {
                        const { component: RouteComponent, children, ...others } = route;

                        return (
                            <Route
                                key={id}
                                {...others}
                                component={props => {
                                    return (
                                        children ? (
                                            <RouteComponent key={id} {...props}>
                                                <ErrorBoundary>
                                                    <Suspense fallback={<PageLoading />}>
                                                        <Switch>
                                                            {children.map((routeChild, idx) => {
                                                                const { path: childPath, ...rest } = routeChild;
                                                                return RouteItem({
                                                                    key: `${id}-${idx}`,
                                                                    path: childPath && path.join(route.path, childPath),
                                                                    ...rest
                                                                })
                                                            })}
                                                        </Switch>
                                                    </Suspense>
                                                </ErrorBoundary>
                                            </RouteComponent>
                                        ) : (
                                                <ErrorBoundary>
                                                    <Suspense fallback={<PageLoading />}>
                                                        {
                                                            RouteItem({
                                                                key: id,
                                                                ...route
                                                            })
                                                        }
                                                    </Suspense>
                                                </ErrorBoundary>
                                            )
                                    )
                                }}
                            ></Route>
                        )
                    })
                }
            </Switch>
        </Router>
    )
}
```
首先，我们用的是HashRouter，当然，你也可以选择BrowserRouter。
然后，遍历routes数组，先创建`<Route>`组件，然后根据数组对象是否包含`children`，来决定是否创建子路由。
函数`RouteItem`提供创建子路由的能力，它会根据`redirect`属性判断是否使用重定向路由组件，并根据用户状态信息，为路由鉴权（这部分内容我们会在下一节中展开描述）。

至此，一个较为完整的SASS平台路由搭建和页面基础布局完成。后续，就可以开心的创建独立的子页面了。