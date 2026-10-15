hummer 内核构建包（KernelSU 编入 + SuSFS v2.3.0）
给一加 Ace 5 Pro（hummer / PKR110）上正在跑的 crDroid 13（Android 17）内核做的复刻构建：
源码 = crDroid 官方内核仓库 17.0 分支、与手机当前内核完全相同的提交（48baf0c723f8）；
配置 = 从手机 boot.img 提取的原始配置，只多了 CONFIG_KSU 与 CONFIG_KSU_SUSFS 两项。
本地已预演通过：两个补丁共 53 个文件零失败、配置解析通过、SuSFS 子功能 10 项全开。
你要做的（GitHub 网页上，约 5 分钟）
新建仓库：GitHub 右上角 + → New repository，名字随便（如 hummer-kernel），选 Public，点 Create。
传配置文件：在仓库页面点 "uploading an existing file"，把本包里的 device.config 传上去，Commit。
建 workflow：点 "creating a new file"，文件名填 .github/workflows/build.yml，
把本包里 build.yml 的全部内容粘进去，Commit。
运行：仓库上方 Actions 页签 → 左侧选 "build-hummer-susfs-kernel" → Run workflow → 绿色 Run workflow。
（第一次进 Actions 可能要先点一下启用 workflows。）
等它跑完（绿色对勾），在运行页面最下面 Artifacts 里下载 AK3-hummer-kernel，
解压得到 AK3-hummer-crdroid17-ksu-susfs.zip。
重要
下载的 AK3 zip 先发给 Muse 验（查版本串和 SuSFS 标记），验过再刷，不要直接刷。
刷之前确认 boot-stock-backup.img 和 init_boot-lkm-backup.img 还在电脑 Downloads 里（救砖用）。
构建若中途变红失败，把失败步骤的日志截图发 Muse，不要反复重跑。
