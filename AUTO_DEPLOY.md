# 全自动部署指南

## 🚀 只需 2 步配置

### 第 1 步：配置 GitHub Secrets

访问：https://github.com/debbide/nav-dashboard/settings/secrets/actions

添加 **2 个 Secrets**：

#### 1. CLOUDFLARE_API_TOKEN

1. 访问：https://dash.cloudflare.com/profile/api-tokens
2. 点击 **Create Token**
3. 使用模板 **Edit Cloudflare Workers**
4. 或自定义权限（推荐）：
   - Account - Workers Scripts - Edit
   - Account - Cloudflare Pages - Edit
   - Account - D1 - Edit
   - Account - Workers KV Storage - Edit
5. 点击 **Create Token**
6. 复制 Token

添加到 GitHub：
- Name: `CLOUDFLARE_API_TOKEN`
- Secret: 粘贴 Token

#### 2. CLOUDFLARE_ACCOUNT_ID

1. 访问：https://dash.cloudflare.com
2. 右侧可以看到 **Account ID**
3. 复制此 ID

添加到 GitHub：
- Name: `CLOUDFLARE_ACCOUNT_ID`
- Secret: 粘贴 Account ID

---

### 第 2 步：运行部署

1. 访问：https://github.com/debbide/nav-dashboard/actions
2. 选择 **Deploy to Cloudflare (全自动)**
3. 点击 **Run workflow** → **Run workflow**

---

## ✨ 自动化内容

GitHub Actions 会自动完成：

1. ✅ **检查 D1 数据库** - 不存在则自动创建
2. ✅ **初始化数据库** - 自动执行 schema.sql
3. ✅ **检查 KV 命名空间** - 不存在则自动创建
4. ✅ **更新配置文件** - 自动填写资源 ID
5. ✅ **部署 Workers** - 自动部署后端 API
6. ✅ **部署 Pages** - 自动部署前端

---

## ⚙️ 首次部署后的一次性配置

部署完成后，需要在 Cloudflare Dashboard **手动配置一次** Pages 绑定：

1. 访问：https://dash.cloudflare.com
2. 进入 **Pages** → **nav-dashboard**
3. 点击 **Settings** → **Functions**
4. 添加 **D1 database binding**:
   - Variable name: `DB`
   - D1 database: 选择 `nav-dashboard-db`
5. 添加 **KV namespace binding**:
   - Variable name: `KV`
   - KV namespace: 选择包含 `nav-images` 的命名空间
6. 点击 **Save**

配置完成后，**以后所有部署都是全自动的**，无需任何手动操作！

---

## 🎉 完成

现在访问：
- **主页**：https://nav-dashboard.pages.dev
- **管理后台**：https://nav-dashboard.pages.dev/admin.html

---

## 🔄 后续更新

以后只需要：
1. 修改代码
2. 推送到 GitHub
3. 自动部署 ✨

无需任何配置！

---

## 📊 资源管理

查看已创建的资源：
- D1 数据库：https://dash.cloudflare.com → D1
- KV 命名空间：https://dash.cloudflare.com → Workers → KV
- Pages 项目：https://dash.cloudflare.com → Pages

---

## ❓ 常见问题

### Q: 部署失败？
A: 检查 Secrets 是否正确配置，API Token 权限是否足够

### Q: Pages 显示错误？
A: 确认已在 Dashboard 配置 D1 和 KV 绑定

### Q: 如何删除所有资源重新部署？
A: 
1. 在 Cloudflare Dashboard 删除 D1 数据库和 KV 命名空间
2. 重新运行 GitHub Actions
3. 自动重新创建所有资源
