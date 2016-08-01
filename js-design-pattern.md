# 代理模式
一个对象充当另外一个对象的接口。

通过包装一个对象以控制对它的访问，其主要方法是将访问聚集为组或者仅当真正必要的时候才执行访问，从而避免了高昂的操作开销。

    var proxy = {
        ids: [],
        delay: 50,
        timeout: null,
        callback: null,
        context: null,
        makeRequest: function (id, callback, context) {

            // add to the queue
            this.ids.push(id);

            this.callback = callback;
            this.context  = context;

            // set up timeout
            if (!this.timeout) {
                this.timeout = setTimeout(function () {
                    proxy.flush();
                }, this.delay);
            }
        },
        flush: function () {

            http.makeRequest(this.ids, "proxy.handler");

            // clear timeout and queue
            this.timeout = null;
            this.ids = [];

        },
        handler: function (data) {        
            var i, max;

            // single video
            if (parseInt(data.query.count, 10) === 1) {
                proxy.callback.call(proxy.context, data.query.results.Video);
                return;
            }

            // multiple videos
            for (i = 0, max = data.query.results.Video.length; i < max; i += 1) {
                proxy.callback.call(proxy.context, data.query.results.Video[i]);
            } 
        }
    };