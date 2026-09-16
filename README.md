# 雷系鈴鐺研究所官方網站

正式網址：https://raibelllab.github.io/

此倉庫只保存建置完成的靜態網站。推送至 main 後，GitHub Actions 會直接發布至 GitHub Pages，不需要 Hugo、Astro 或 Node.js 建置環境。

## 更新網站

1. 在開發專案建置正式版：

   ```sh
   cd /Users/raichan/Home/raibelllab.github.io-dev
   env -u DEMO npm run build
   ```

2. 將 dist/ **內部所有檔案與資料夾**放到本倉庫根目錄，不要多包一層 dist。包含 _astro/、images/ 與各語系目錄，排除 .DS_Store。
3. 替換前移除舊網站檔案，避免已刪除的頁面與舊資源殘留。務必保留 .git/、.github/、.gitignore、.nojekyll 與 README.md。不要上傳 src/、node_modules/、開發設定或機密檔案。
4. 用 Fork 或 Git 提交全部新增、修改及刪除項目，推送至 main。
5. 在 GitHub Actions 確認「發布靜態網站至 GitHub Pages」成功，再檢查正式網站。

可用以下指令代替步驟 2、3；執行前請確認正式建置成功，且來源與目的目錄正確：

```sh
rsync -av --delete \
  --exclude='.git/' --exclude='.github/' \
  --exclude='.gitignore' --exclude='.nojekyll' --exclude='README.md' \
  --exclude='.DS_Store' \
  /Users/raichan/Home/raibelllab.github.io-dev/dist/ \
  /Users/raichan/Home/raibelllab.github.io/
```

注意：build:demo 也輸出至 dist/，但使用不同網址與路徑；正式發布前必須重新執行上述正式建置。

## GitHub Pages 設定

Settings → Pages → Source 保持 GitHub Actions。部署流程位於 .github/workflows/static.yml。

## 還原

Git 歷史保留舊 Hugo 網站。需要還原時，透過 Git revert 還原對應部署提交並推送；不需要刪除倉庫或強制推送。
