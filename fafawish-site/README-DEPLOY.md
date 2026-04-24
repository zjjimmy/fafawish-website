# fafawish 网站部署指南

## 方法：GitHub + Vercel（推荐）

### 第一步：创建 GitHub 仓库

1. 打开 https://github.com/new
2. Repository name 填写：`fafawish-website`
3. 选择 **Public**（免费）
4. 勾选 **Add a README file**
5. 点击 **Create repository**

### 第二步：上传网站文件

**方法 A：直接在 GitHub 网页上传**
1. 进入刚创建的仓库页面
2. 点击 **Add file** → **Upload files**
3. 把 `fafawish-site` 文件夹里的所有文件拖进去
4. 点击 **Commit changes**

**方法 B：用 Git 命令（如果你有安装 Git）**
```bash
# 进入网站文件夹
cd fafawish-site

# 初始化 git
git init

# 添加所有文件
git add .

# 提交
git commit -m "Initial commit"

# 关联远程仓库（用你的实际仓库地址）
git remote add origin https://github.com/你的用户名/fafawish-website.git

# 推送
git push -u origin main
```

### 第三步：Vercel 自动部署

1. 打开 https://vercel.com/new
2. 点击 **Import Git Repository**
3. 找到 `fafawish-website` 仓库，点击 **Import**
4. Project Name 填写：`fafawish`
5. Framework Preset 选择：**Other**
6. 点击 **Deploy**

等待 1-2 分钟，Vercel 会给你分配一个临时域名（如 `fafawish-xxx.vercel.app`）

### 第四步：绑定你的域名

1. 在 Vercel 项目页面，点击 **Settings** → **Domains**
2. 输入你的域名，点击 **Add**
3. Vercel 会显示 DNS 记录配置
4. 去你的域名服务商（阿里云/腾讯云/GoDaddy 等）添加 DNS 记录：
   - Type: `CNAME`
   - Name: `www` 或 `@`
   - Value: `cname.vercel-dns.com`

等待 DNS 生效（通常 5-30 分钟）

---

## 备选方案：直接给我域名，我帮你检查

如果你告诉我域名是什么，我可以：
1. 检查 DNS 配置是否正确
2. 确认网站是否正常访问
3. 帮你排查问题

---

## 常见问题

**Q: 图片不显示？**
A: 确保 `images/` 文件夹也在 GitHub 仓库里

**Q: 备案问题？**
A: Vercel 服务器在海外，不需要备案。如果域名在国内服务商购买的，可能需要实名认证。

**Q: 访问慢？**
A: 国内访问 Vercel 可能较慢。如需加速，可以考虑：
- 阿里云 OSS + CDN（需要备案）
- 腾讯云 COS + CDN（需要备案）
- 或者使用 Cloudflare 加速
