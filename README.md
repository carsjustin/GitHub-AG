# Auto-Green

[![Build Status](https://github.com/carsjustin/GitHub-AG/workflows/GitHub-AG/badge.svg?branch=main)](https://github.com/carsjustin/GitHub-AG/actions)

自動保持 GitHub 提交狀態常綠。

> A commit a day keeps your girlfriend away!

## 發想

使用 GitHub Actions 的定時任務功能，每隔一段時間自動執行 `git commit`，提交信息為 "A commit a day keeps your girlfriend away!"，靈感来自知乎問題[在 GitHub 上保持 365 天全綠是怎樣一種體驗？](https://www.zhihu.com/question/34043434/answer/57826281)下某匿名用戶的回答：

> 曾經保持了 200 多天全綠，但是冷落了女朋友，一直綠到現在。

## 原理

有關 Github Action 的原理，可查看官方文檔 [Github Action 簡介](https://docs.github.com/cn/actions/learn-github-actions/introduction-to-github-actions)

## 如何使用

- 點右上角 **Use this template** 按鈕複製本 GitHub 倉庫，**:warning: 千萬不要 Fork，因為 fork 項目的動態並不會讓你變綠 :warning:**
- 修改 [GitHub-AG.yml 文件的第 8、9 行](https://github.com/carsjustin/GitHub-AG/blob/master/.github/workflows/GitHub-AG.yml#L8-L9) 去掉前面的 `#` 號
- 修改 [GitHub-AG.yml 文件的第 20、21 行](https://github.com/carsjustin/GitHub-AG/blob/master/.github/workflows/GitHub-AG.yml#L20-L21) 為自己的 GitHub 帳號和名稱
  - 方法1: 將 **${{secrts.EMAIL}}** 改成 **"你的電子郵件(要包括引號)"** , **${{secrets.NAME}}** 改成 **"你的GitHub名字(要包括引號)"**
  - 方法2: 前往此倉庫的**設定** - **Secret** - **Actions** - **New repositories secret**, **Name填EMAIL** ,**Value填你的電子郵件** ,再新增一個 **Name填NAME** ,**Value填你的GitHub名字**  方法2的好處是能隱藏Email,避免個資外洩!
- (可選) 你可以通過修改 [GitHub-AG.yml 文件的第 8 或 9 行](https://github.com/carsjustin/GitHub-AG/blob/master/.github/workflows/GitHub-AG.yml#L8-L9)來調整頻率

計畫任務語法有 5 個字段，中間用空格分隔，每個字段代表一个時間單位

```plain
┌───────────── 分鐘 (0 - 59)
│ ┌───────────── 小時 (0 - 23)
│ │ ┌───────────── 日 (1 - 31)
│ │ │ ┌───────────── 月 (1 - 12 或 JAN-DEC)
│ │ │ │ ┌───────────── 星期 (0 - 6 或 SUN-SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
```

每個時間字段的含意

|符號   | 描述        | 舉例                                        |
| ----- | -----------| -------------------------------------------|
| `*`   | 任意值      | `* * * * *` 每天每小時每分鐘                  |
| `,`   | 值分隔符    | `1,3,4,7 * * * *` 每小時的 1 3 4 7 分鐘       |
| `-`   | 範圍       | `1-6 * * * *` 每小時的 1-6 分鐘               |
| `/`   | 每         | `*/15 * * * *` 每隔 15 分鐘                  |

**頻率修改範本**
- 修改為 0 * * * *      代表每小時執行一次
- 修改為 0 */4 * * 1-5  代表每週一到周五 每4小時執行一次
- 修改為 0 */12 * * 6   代表每週六 每12小時執行一次
- 修改為 0 * * * 1-5    代表每週一到週五 每小時執行一次
- 修改為 0 */8 * * 0,6  代表每週六和週日 每8時執行一次
- 修改為 0 */3 * * 1-5  代表每週一到週五 每3小時執行一次
- 修改為 0 */8 * * 6    代表每週六 每8小時執行一次
- 修改為 0 */12 * * 0   代表每周日 每12小時執行一次
- 不了解如何設定頻率可以使用下方頻率產生器

**註**：由於 GitHub Actions 的限制，如果設置為`* * * * *` 實際的執行頻率為每 5 分鐘執行一次

**頻率產生器**
- [Crontab Generator](https://crontab-generator.org/)
- [crontab guru](https://crontab.guru/)
- [Cron expression generator by Cronhub](https://crontab.cronhub.io/)
- [Cron Expression Generator & Explainer - Quartz](https://www.freeformatter.com/cron-expression-generator-quartz.html)


## License

[Auto-Green](https://github.com/justjavac/auto-green) is released under the MIT License. See the bundled [LICENSE](./LICENSE) file for details.
