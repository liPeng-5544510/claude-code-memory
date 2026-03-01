# 浏览器书签清理经验

## 问题场景
用户想要删除失效的网页收藏（书签）

## 成功部分
- 直接读取 Edge 书签文件：`C:\Users\{username}\AppData\Local\Microsoft\Edge\User Data\Default\Bookmarks`
- JSON 格式解析，并发检测 URL 有效性（ThreadPoolExecutor）
- 检测逻辑工作正常：460 个书签检测出 185 个失效

## 失败原因
**Edge 云端同步覆盖了本地修改**

现代浏览器（Chrome/Edge）默认开启书签云同步：
1. 替换本地 `Bookmarks` 文件
2. 用户打开浏览器后，云端同步会自动覆盖本地文件
3. 用户看到的书签没有任何变化

## 正确做法
1. **先检查是否开启同步** - 询问用户或检查浏览器设置
2. **如果开启同步**：
   - 方案A：先关闭同步 → 修改本地 → 再开启同步（会覆盖云端）
   - 方案B：直接在浏览器中手动删除（浏览器会同步删除到云端）
   - 方案C：使用浏览器扩展/脚本来批量删除
3. **如果未开启同步**：直接替换本地文件即可

## Edge 书签文件路径
```
C:\Users\{username}\AppData\Local\Microsoft\Edge\User Data\Default\Bookmarks
```

## Chrome 书签文件路径
```
C:\Users\{username}\AppData\Local\Google\Chrome\User Data\Default\Bookmarks
```

## 文件格式
- JSON 格式，包含 `bookmark_bar`、`other`、`synced` 三个根节点
- 每个书签有唯一 `guid` 字段用于标识
