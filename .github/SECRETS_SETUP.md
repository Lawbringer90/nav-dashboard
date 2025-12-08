# GitHub Secrets 配置指南

部署需要在 GitHub 仓库中配置以下 Secrets。

## 📋 需要的 Secrets

访问：https://github.com/debbide/nav-dashboard/settings/secrets/actions

依次添加以下 4 个 Secrets：

---

### 1. CLOUDFLARE_API_TOKEN

**获取步骤**：

1. 访问 https://dash.cloudflare.com/profile/api-tokens
2. 点击 **Create Token**
3. 选择模板 **Edit Cloudflare Workers**
4. 或者自定义权限：
   - **Account** - Cloudflare Pages - **Edit**
   - **Account** - D1 - **Edit**
   - **Account** - Workers Scripts - **Edit**
5. 点击 **Continue to summary**
6. 点击 **Create Token**
7. **复制** 显示的 Token（只显示一次！）

**在 GitHub 中添加**：
- Name: `CLOUDFLARE_API_TOKEN`
- Secret: 粘贴刚才复制的 Token

---

### 2. CLOUDFLARE_ACCOUNT_ID

**获取步骤**：

1. 访问 https://dash.cloudflare.com
2. 右侧侧边栏可以看到 **Account ID**
3. 点击复制图标

**在 GitHub 中添加**：
- Name: `CLOUDFLARE_ACCOUNT_ID`
- Secret: 粘贴 Account ID（类似：`a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6`）

---

### 3. D1_DATABASE_ID

**获取步骤**：

已在 `wrangler.toml` 中配置：`110c9d6b-52d7-4d2c-876b-1c6ba08f22d4`

**在 GitHub 中添加**：
- Name: `D1_DATABASE_ID`
- Secret: `110c9d6b-52d7-4d2c-876b-1c6ba08f22d4`

---

### 4. R2_PUBLIC_ID

**获取步骤**：

已在 `wrangler.toml` 中配置：`f249af155623469d94c5404717ea3888.r2.dev`

**在 GitHub 中添加**：
- Name: `R2_PUBLIC_ID`
- Secret: `f249af155623469d94c5404717ea3888.r2.dev`

---

## ✅ 配置完成后

1. 访问：https://github.com/debbide/nav-dashboard/actions
2. 选择 **Deploy to Cloudflare** workflow
3. 点击 **Run workflow** → **Run workflow**
4. 等待部署完成 ✅

---

## 🔍 验证配置

确保添加了这 4 个 Secrets：
- ✅ CLOUDFLARE_API_TOKEN
- ✅ CLOUDFLARE_ACCOUNT_ID  
- ✅ D1_DATABASE_ID
- ✅ R2_PUBLIC_ID

全部配置完成后，每次推送代码到 main 分支都会自动部署！🚀
