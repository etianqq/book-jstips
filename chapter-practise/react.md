## React练习题

#### 1. setState
 
```
import React from "react";

class TestView extends React.Component {
  state = {
    count: 0,
  };
  componentDidMount() {
    this.setState({
      count: this.state.count + 1,
    });
    console.log("console: " + this.state.count);

    this.setState({ count: this.state.count + 1 }, () => {
      console.log("console from callback: " + this.state.count);
    });

    this.setState(
      (prevState) => {
        console.log("console from func: " + prevState.count);
        return {
          count: prevState.count + 1,
        };
      },
      () => {
        console.log("last console: " + this.state.count);
      }
    );
  }

  render() {
    console.log("render" + this.state.count);
    return <h4>test</h4>;
  }
}

export default TestView;

```