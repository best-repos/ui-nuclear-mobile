# PullToRefresh 拉动刷新

通过触发，立刻重新加载内容。

### 规则
 * 可以和 ListView 结合使用，也可以单独使用。
 * 可考虑定期自动刷新, e.g. 登录 APP 后，自动刷新首页 List。


### props

| 属性 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
|  distanceToRefresh  | 刷新距离 | number | 25 |
|  direction  | 拉动方向，可以是 `up` 或 `down` | String | `down` |
|  indicator  | 指示器配置 | Object `{ activate: '', deactivate: '', release: '', finish: '' }` | - |
|  refreshing  | 是否显示刷新状态	 | bool | false |
|  onRefresh  | 必选, 刷新回调函数 | function | - |