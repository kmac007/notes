# <form>标签用于用户输入创建HTML表单
> 表单能够包含 input 元素，比如文本字段、复选框、单选框、提交按钮等等。表单还可以包含 menus、textarea、fieldset和label元素。
表单用于向服务器传输数据
## <form> 属性

属性 | 值 | 描述
---|---|---
action | URL | 规定当提交表单时向何处发送表单数据
autocomplete | on off | 规定是否启用表单的自动完成功能
method | get post | 规定用于发送form-data的HTTP方法
name | form_name | 规定表单名称
enctype | application/x-www-form-urlencoded \|\| multipart/form-data \|\| text/plain | 规定在发送表单数据之前如何对其进行编码。
## <input>
### text, password, submit
```
<form action="form_action.php" method="get">
    用户名：<input type="text" name="username">
    密码：<input type="password" name="password">
    <input type="submit" value="submit">
</form>
```
### checkbox
```
<form action="form_action.php" method="get">
    汽车: <input type="checkbox" name="Car">
    飞机: <input type="checkbox" name="Plane" checked="checked">
</form>
```
### radio
```
<form action="form_action.php" method="get">
    男：<input type="radio" checked="checked" name="Sex" value="male">
    女: <input type="radio" name="Sex" value="female">
</form>
```
## <select>
```
<form>
    <select name="city">
        <option value="shanghai">上海</option>
        <option value="beijing">北京</option>
        <option value="guangzhou">广州</option>
        <option value="shenzhen" selected>深圳</option>
    </select>
</form>
```
## <textarea>
```
<textarea rows="10" cols="30">
```
## <button>
```
<form>
    <button type="submit">提交</button>
</form>
```

