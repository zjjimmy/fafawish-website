# fafawish 网站部署指南 — Vercel + jimiwell.cn

## 域名状态
- 域名：jimiwell.cn
- 状态：未备案
- 方案：Vercel（海外服务器，无需备案）

---

## 第一步：上传代码到 GitHub

### 1.1 创建 GitHub 仓库
1. 打开 https://github.com/new
2. Repository name：`fafawish-website`
3. 选择 **Public**
4. 勾选 **Add a README file**
5. 点击 **Create repository**

### 1.2 上传网站文件
1. 进入仓库 https://github.com/你的用户名/fafawish-website
2. 点击 **Add file** → **Upload files**
3. 进入 `F:\MyFile\Desktop\fafawish-site\` 文件夹
4. **全选所有文件**（包括 images 文件夹、index.html、vercel.json）
5. 拖入 GitHub 上传区域
6. 点击 **Commit changes**

> ⚠️ 重要：必须包含 images 文件夹，否则图片无法显示！

---

## 第二步：Vercel 自动部署

### 2.1 登录 Vercel
1. 打开 https://vercel.com
2. 点击 **Sign Up** → 选择 **Continue with GitHub**
3. 授权 Vercel 访问你的 GitHub 仓库

### 2.2 导入项目
1. 打开 https://vercel.com/new
2. 找到 `fafawish-website` 仓库，点击 **Import**
3. Project Name：`fafawish`
4. Framework Preset：**Other**
5. Root Directory：`./`（默认）
6. 点击 **Deploy**

等待 1-2 分钟，网站会自动部署。Vercel 会给你一个临时域名，例如：
`https://fafawish-xxx.vercel.app`

---

## 第三步：绑定域名 jimiwell.cn

### 3.1 在 Vercel 添加域名
1. 进入 Vercel 项目 Dashboard
2. 点击顶部 **Settings** 标签
3. 左侧选择 **Domains**
4. 输入域名：`jimiwell.cn`
5. 点击 **Add**
6. Vercel 会显示 DNS 配置信息：

```
Type: A
Name: @ (或 jimiwell.cn)
Value: 76.76.21.21

Type: CNAME  
Name: www
Value: cname.vercel-dns.com
```

### 3.2 在阿里云配置 DNS
1. 登录阿里云控制台 https://dns.console.aliyun.com
2. 找到 `jimiwell.cn` 域名，点击 **解析设置**
3. 添加两条记录：

**记录 1（根域名）：**
- 记录类型：A
- 主机记录：@
- 解析线路：默认
- 记录值：76.76.21.21
- TTL：10分钟

**记录 2（www 子域名）：**
- 记录类型：CNAME
- 主机记录：www
- 解析线路：默认
- 记录值：cname.vercel-dns.com
- TTL：10分钟

4. 点击 **确认**

### 3.3 等待生效
- DNS 生效时间：通常 **5-30 分钟**
- 在 Vercel Domains 页面可以看到状态：
  - ❌ Invalid Configuration → DNS 未生效，等待
  - ✅ Valid Configuration → 绑定成功！

---

## 第四步：验证网站

1. 打开浏览器访问 https://jimiwell.cn
2. 应该能看到 fafawish 网站
3. 检查所有图片是否正常显示
4. 点击导航链接测试页面滚动

---

## 常见问题

### Q: 图片不显示？
A: 检查 GitHub 仓库里是否有 images 文件夹，确认所有图片已上传。

### Q: 访问慢？
A: Vercel 服务器在海外，国内访问可能稍慢。如需加速：
- 方案1：使用 Cloudflare CDN（在阿里云 DNS 切换到 Cloudflare 解析）
- 方案2：备案后用阿里云 OSS（国内速度最快）

### Q: 如何更新网站？
A: 修改本地文件 → 重新上传到 GitHub → Vercel 自动重新部署（约 1 分钟）

### Q: 需要 HTTPS？
A: Vercel 自动提供 HTTPS 证书，无需额外配置。

---

## 紧急备案通道（可选）

如果未来需要备案（.cn 域名建议备案）：
1. 阿里云备案系统：https://beian.aliyun.com
2. 需要：阿里云服务器（最低¥99/年）
3. 备案时间：约 7-20 个工作日
4. 备案后：切换到阿里云 OSS / ECS，国内访问速度提升 3-5 倍
