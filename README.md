### git小遊戲
Learn Git Branching
https://learngitbranching.js.org/?locale=zh_TW

### 工作目錄
### 暫存區
暫存區進度會 >= 儲存庫，即使檔案commit到儲存庫，在暫存區也不會消失
### 儲存庫
#### git init
#### git status
新建檔案，檔案還未被追蹤<br/>
兩段式設計（幫助作挑選，過濾不需要的）
#### add
* 將特定檔案加入：
git add a.html(檔案名稱) ---> a.html已被追蹤
* 一次加入多個檔案
1. git add . 將當前資料夾內的檔案加入
2. git add --all or git add -A 將當前螢幕上所有檔案（不管在哪個資料夾）都加入

#### commit
git commit -m 'init commit'(訊息一定要有)
* commit訊息（參考約定式提交）<br/>
build:
chore:
refactor:
docs:
style:
perf:
test:

#### 復活檔案（從暫存區救）
git restore b.html(要救回的檔案)
git restore . 危險⚠️可以將所有刪除的檔案就回但是現有檔案（還沒加到暫存區的）會回復到編輯以前的狀態（空的）

git log看過去commit紀錄<br/>
git log --oneline 簡化指令，更好閱讀

#### 分支branch
git branch 查看所有分支<br/>
git branch cat(要新增的分支名稱)<br/>
git branch -d cat(要刪除的分支名稱)<br/>
-砍掉後的分支如果要救回，要記住當時Commit的位置e.g.053fb212<br/>
git branch cat 053<br/>
git branch -m 'ccc' 將目前分之名稱更改為ccc<br/>
git switch dog(要切換過去的分支名稱)<br/>
👴git checkout 可切分支也可救檔案，模糊地帶<br/>
    -git switch切分支<br/>
    -git restore救檔案<br/>
git switch - 適用在兩個分支一直來回切換
#### 合併merge, bebase
1. merge 
- 會保留歷史軌跡
- git merge dog(我目前所在分支要合併dog分支)
舊分支合併新分支，反之行不通
Fast-forward快進合併
2. rebase 重訂基底(建議使用)
- 歷史軌跡乾淨
- git rebase dog(我要合進去到dog分支，合進去後git graph線條從Y變I一條線，我現在分支名稱會在dog上面)
- git rebase -i ca40(座標)
p -> pick使用提交<br/>
r -> reword使用提交，但繼續編輯<br/>
e -> edit 使用提交，但不直接修補（amend）<br/>
s -> sqush 使用提交，但融交至上個提交<br/>
f -> fixup<br/>
git rebase --abort取消此次的rebase行為

#### reset
* git reset 座標 （我想要變成/退回 座標 那個樣子）
假設從3退回1，那3,2新增/變更的檔案要去哪裡呢？
--mixed 工作目錄（預設）<br/>
--soft 暫存區<br/>
--hard 不要了<br/>
git reset HEAD^ --hard 變成現在的前一步(往第一個parent移動)<br/>
git reset HEAD~2 --hard 退兩步（往第二個parent移動）<br/>
git reset HEAD~50 --hard 退50步<br/>
^ :caret 有方向性<br/>
~ :tilde 沒有方向性，都是往第一個parent移動
* git reset ORIG_HEAD
回到最近一次重大的危險操作（reset, rebase....）

#### git reflog✨
可看到HEAD的移動紀錄，使用時機：搭配reset使用 ---> 無敵🚩

* 如果雙方有衝突，解衝突的錯誤做法：
git add 有衝突的檔案<br/>
git commit -m ''
雖然這樣會解決衝突，但是檔案內仍存在兩者待解的衝突畫面

#### git blame
可以抓出某一行的作者(兇手)是誰

#### git help

#### 歷史紀錄的修正
git commit --amend
1. 假設我發了一個指令：git commit -m 'add fish.html'
2. 後來我又新增了一個fish2.html，我不希望再增加一個commit紀錄（影響版面），我希望fish.html & fish2.html出現在同一個commit紀錄裡面，這時候可以
- git add fish2.html
- git commit --amend
3. 此時，fish2.html會被加到add fish.html那次的commit紀錄裡面