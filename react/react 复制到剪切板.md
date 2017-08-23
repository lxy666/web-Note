## React复制到剪贴板可以使用插件copy-to-clipboard

[参考API文档](https://www.npmjs.com/package/react-copy-to-clipboard)

## 安装
```
npm install --save react react-copy-to-clipboard
```

## 使用
```

const App = React.createClass({
  getInitialState() {
    return {value: '', copied: false};
  },


  onChange({target: {value}}) {
    this.setState({value, copied: false});
  },


  onCopy() {
    this.setState({copied: true});
  },


  render() {
    return (
      <div>
        <h1>CopyToClipboard</h1>

        <input value={this.state.value} size={10} onChange={this.onChange} /> 

        <CopyToClipboard text={this.state.value} onCopy={this.onCopy}>
          <span>Copy to clipboard with span</span>
        </CopyToClipboard> 

        <CopyToClipboard text={this.state.value} onCopy={this.onCopy}>
          <button>Copy to clipboard with button</button>
        </CopyToClipboard> 


        {this.state.copied ? <span style={{color: 'red'}}>Copied.</span> : null}

        <br />

        <textarea style={{marginTop: '1em'}} cols="22" rows="3" />

      </div>
    );
  }
});

const appRoot = document.createElement('div');

appRoot.id = 'app';
document.body.appendChild(appRoot);
ReactDOM.render(<App />, appRoot);
```


![演示](http://upload-images.jianshu.io/upload_images/3229842-7a6a0942e56edc92.gif?imageMogr2/auto-orient/strip)



