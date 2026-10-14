## day1学习记录
- Linux常用命令10条手敲+看帮助，熟悉熟悉以前学过的命令，发现head跟tail其实是单独的命令，在和cat等查看文档方面命令是需要使用“|”隔开。
- GitHub构建仓库qa-practice，成功踩坑后才正常上传。
- 仓库里放置README.md与notes目录，通过撰写学习记录，记录自己的学习情况。
## D1踩坑记录：root上传事件（10/12晚）
 **agent实际检查：**
- 仓库建立在root家目录（/root/qa-practice），属主为root；没有配置任何GitHub远端->因此每天上传成功。
- GitHub（hoshinoick811）下没有qa-practice仓。
- 先前配置过commit作者，就是hoshinoick811；GitHub ssh钥配好且验证通过

- 修复步骤
1. 退出root会话:cd ~，然后exit；whoami显示为hoshinoick811
2. 将仓库搬回自己家并过户：
```bash
 sudo mv /root/qa-practice ~/qa-practice
 sudo chown -R hoshinoick811:hoshinoick811 ~/qa-practice
 ls -la ~/qa-practice
```
3. 验证仓库完整性：cd ~/qa-practice && git log --oneline && git status
4. GitHub上新建空仓库，与本地文件夹同名。
5. 接上远端并推送：`git remote add origin git@github.com:hoshinoick811/qa-practice.git`,然后`git push -u origin main`
6. 验收：`git remote -v`；看到两个正确的提交。

## 两条教训：
- **练习时一律使用自己的账户**：root只做系统管理。github钥放在自己账户，root没有，推不上去。
- **“以为自己传了”≠“验证过后再传”**：验收标准永远是对面能打开，测试工作常用。
