# Git 操作指令介紹

Git 是一種版本控制系統的軟體，所謂「版本控制系統」是一種對於原始程式碼修訂的歷程做完整性的紀錄，並且透過軟體來比對、控制及管理原始程式碼版本與版本之間的差異性。在開發大型的軟體系統過程，是由多位程式設計師共同來開發，並且需要不斷地測試、修正原始程式碼，對於原始程式碼之間的差異性，就特別需要像 Git, SVN 等版本控制系統軟體來處理多人、不同版本之間的差異性，在這樣的開發環境下，分享原始程式碼是必要的條件，一般是架設網站來儲存、分享、管理原始程式碼，不同版本控制系統有相對應的網站伺服器軟體，目前常見的軟體有 Git, SVN, Mercurial等，而針對 git 版本控制系統提供服務的網站有 github, bitbuck gitLab，這些網站都可以免申請，向 github or bitbucket 網站申請帳號以後，需要先登入 github or bitbucket 網站 create 一個 project repository，然後 git clone 回 local repository，開始撰寫、修改原始程式碼，再把原始程式碼儲存到 local repository， 最後 git add, git commit and git push 到 remote repository 內部。

若想要先在 local repository 建立一個 project， git init 以後，再把原始程式碼 upload 到 remot repository 裡面，這樣的做法不需要先登入 github or bitbucket，使用 github or bitbucket 網頁式的 App 去 new a repository，在[stackoverflow 這篇文章][1]提到網路上有人開發 [hub 軟體][2]來處理，不過需要 Go 的開發環境，我選擇使用 [cURL 這個工具程式][3]來處理這個問題，必且是在 ASUS T200TA Transformer on 32-bits Windowns 8 system 的環境測試成功。

[1]: https://stackoverflow.com/questions/2423777/is-it-possible-to-create-a-remote-repo-on-github-from-the-cli-without-opening-br "CLi create remote repository"
[2]: https://hub.github.com/ "Hub 網站"
[3]: https://curl.haxx.se/ "cURL 網站"

採用 cURL create github  repository 的步驟:

1 Download cURL for 32-bits windows system from [cURL 網站][3]

2 設定 cURL 執行的環境變數

3 curl -u elvishsieh https://api.github.com/user/repos -d "{\"name\": \"testing\"}"

4 輸入 github 登入的密碼

5 連結到 github.com/username 檢查 testing 的 repository 是否已經被建立?

建立 github 的 repository 以後，在 local directory 也必須建立 local repository，用來存放自己開發的原始程式碼，等到自己的程式碼都測試完成，再上傳的剛剛在 github 網站建立的 testing repository，其實際的操作步驟如下：

1 建立新目錄及加入 README.md 檔案，例如 echo This is first file which name is README.md > README.md

2 Initializing local repository: git init

3 異動檔案以後，更新 work tree 的紀錄: git add . 或者 git add *

4 修改檔案提交到 local repository: git commit -m "message for this commit"

5 新增 remote origin 的 repository : git remote add origin https://github.com/elvishsieh/testing.git

6 上傳 github: git push -u origin master // --set-upstream 

上述描述的內容是簡略的敘述 git 及上傳 github 的過程，依照內容可以快速的建立 local 及 remote repository。然而，git 版本控制仍有許多細節及設定，將依照不同情況，實際操作也有所不同，接下來的文件說明，將依照不同情況，一一描述其實際遭遇的情形以及實際操作的步驟。

## Github pages for your website
[Websites for you and your projects](https://pages.github.com/)

## 設定 global 的帳號

git config --global user.name "elvishsieh"

git config --global user.email "elvis.hsieh@gmail.com"

```cmd
[/d/student/mikcey.github.io] -user- git commit -m "move to baby directory"

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'user@DESKTOP-IO6QNVA.(none)')
```
## New or delete a remote repository

登入 github, or gitLab, or bitbucket remote repository，然後 create 一個新的 repository，在建立新的  repository 時，可以選擇 create README.md or .gitignore files，通常不需要選擇任一項目，讓 repository 是空的，若 repository 當成 web page 時，才不需要特別刪除 README.md 檔案。另外，可以使用 cURL 來建立、刪除 repository，直接 create or delete repository.

```markdown

curl -u elvishsieh https://api.github.com/user/repos -d "{\"name\": \"testing\"}"

curl -u elvishsieh -X DELETE https://api.github.com/repos/elvishsieh/testing
```

## 建立本地的儲存庫

在 remote repository 建完一個新的 repository，緊接著再從這個新的 repository 網址 clone 回 local d:/github directory；從 remote repository clone 回 local directory 以後，這個 local directory 就已經屬於 git local repository，不需要再輸入 git init 指令。假設在 remote repository 新建立的 project 命名為 test，則上述完整的操作指令如下：

```markdown
cd /d d:
mkdir github
cd github
git clone https://github.com/elvishsieh/testing
```

這時候 d:\github\testing 已經是一個 git 的 local repository，現在可以把 clone 回來的原始程式碼或者資料修改、新增、複製的動作，而當初新建 new remote repository 時，若沒有建立任何檔案，也就選擇 .gitignore 的選項，則 cd 到 local repository directory，然後新增  README.md 的檔案，例如：

```markdown
cd /d d:\github\testing
echo "This is a text file which must be named 'READMD.md' for github webiste." > README.md
```

我們也可以從別的 directory 把檔案複製到 d:\github\testing directory，以上對於 local repository 新增 README.md 以及複製新檔案等動作，是對 local repository 做資料異動的操作，此時可以輸入 'git status' 來查看 local repository 資料被異動的情況，對於異動的資料，git ststus 會以紅色表示被異動過的檔案，也表示這些檔案尚未被加入到 local repository 內部，假設所有的資料異動已經告一個段落，希望把異動的資料加入
到 local repository 內，則可以輸入下列指令：

```markdown
git add *
```

雖然 git add * 指令有一些粗暴，但是卻很方便，當然也可以在 git status 以後，僅把紅色的檔案加入到 local repository，例如： git add README.md, or git add . 把目前目錄下的異動過的檔案加入到 local repository 內，特別值得注意的是：如果 del README.md 以後，仍然需要 git add README.md or git add .,因為 git add 是表示把新增、刪除、複製等異動過的檔案加入到 local repository 內部。

把異動過的檔案加入 local repository 內，還需要做 commit 的動作才算真正把異動後的檔案儲存到 local repository。在 git commit 時，會要求對於這次 commit 的動作，撰寫其異動的紀錄，例如：

```markdown
git commit -m "This is commit message for this time."
```

## 更新異動資料到 remote repository

在 local repository 完成 commit 的動作，表示程式設計師對於這次所開發的原始程式碼告一個段落，程式設計師不見得要馬上將這次異動的程式碼 update 到 remote repository 網站，仍然可以對 local repository 內的檔案做新增、修改等異動操作；若對於 local repository 的異動已經大致完成，可以把這些異動 update 到 remote repository 之中，則輸入的指令如下：

```markdown
git push -u origin master
```

上面介紹建新 project 的 repository、建立 local repository、 update remote repository 的過程，所有指令可以總結如下：

```markdown
mkdir github; cd github
git clone https://github.com/elvishsieh/testing
cd testing
echo "testing repository" >> README.md
git add README.md
git commit -m "first commit"
git push -u origin master
```

若在 remote repository 已經建立一個 repository，例如 testing repository, 但不想從 remote repository clone 回 local repository，可以依照下列指令來 upload 異動資料到 remote repository:

```markdown
mkdir testing
cd testing
echo "# testing" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/elvishsieh/testing.git
git push -u origin master
```

不論是否從 remote repository clone 回 local repository 與否，總是得先登入 remote repository 建立新 project 的 repository，如何使用 cURL 或 SSH 軟體直接從 client 端建立 remote repository? 各家 repository 有不同的 command line 指令，若能由 client 端直接建立 remote repository 以後，就可以git init 並且 upload local repository 到 remote repository。

## 更新 local or remote repository

更新 local(or sync) from remote repository 的指令:

1 git pull  // fetch + merge

2 git fetch

更新 remote repository if local files were modified 的步驟:

1 修改 source code or files

2 git add . or git add * or git add modified_file_names

3 git commit -a -m "this is a description for committing this midified code"

4 git push

## Branch 的操作

github 公司提供 github.io/username 網站伺服器，讓使用者可以把儲存在 github.com 的原始程式碼，以網頁的方式呈現在網路上，而要把 github.com 網站的 HTML, Markdown 原始程式碼轉換到 github.io/username/dir 有三種做法：

1 登入 github.com，進入 remote diretory 中做設定，在 Setting  >> GitHub Pages 選項中，把 None 改成 Use the master branch for GitHub Pages.

![Github page Setting](./images/gitpage.png)

2 建立一個 new repository，且名稱必須為 username.github.io/directory

3 建立一個 gh-pages 的 branch：這種做法是希望把原始程式碼與產出的網頁分開儲存

第 1 種作法是直接登入 github 網站，然後如上圖所顯示的設定方式；第 2 種可以參考前面建立一個 new repository 的作法，新增一個 username.github.io 的 repository；第 3 種做法是建立一個 gh-pages branch，假設在 github.com 中已經建立一個 Mobirise 的 repository，並且在 remote repository 已經新增 project repository，以及異動資料也上傳到這個 repository，則：

```markdown
git clone https://github.com/elvishsieh/testing.git
git checkout -b gh-pages
echo gh-pages readme > README.md
git add README.md
git commit -m "commit gh-pages branch"
git push -u origin gh-pages  //or git push --set-upstream origin gh-pages
```

## git checkout and reset

In working directory status:

git checkout .  // discard changes in working directory

>>> you can delete files from working status, but it have been deleted that couldn't recovery it.

We can reset the files when it have been add/commit into repository.

git reset HEAD^

```markdown
 (use "git add/rm <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory)
```
### example for checkout and reset
當 `git clone llvm-mingw(要找正確的 URL)` 以後，可以 `git pull` 來更新' remote repository 的 source code。但是，如果不小心把 local repository 的 folder or files 刪除，有以下兩種情況來恢復 local repository 刪除的 folder or files：

* 尚未 `git add` 到 local repository 的 index 內： `git checkout -- foldername or filenames`

* 已經 `git add` 把 index 加入 local repository index 內：
   1. git reset
   2. git checkout -- foldername or filenames

同樣的觀念，如果在 llvm-mingw Project 內修改程式碼，修改後輸入 `git status` 會顯示被修改的檔名，如果要再次恢復與 remote repository 的程式碼，則可以先把 local repository 內修改的檔案刪除，再使用 `git checkout`指令來恢復與 remote repository 內的程式碼。
 
## FAQ

在 git help commit 說明文件中提到:

Commit log messages are typically encoded in UTF-8, but other extended ASCII encodings are also supported. This includes ISO-8859-x, CP125x and many others, but not UTF-16/32, EBCDIC and CJK multi-byte encodings (GBK, Shift-JIS, Big5, EUC-x, CP9xx etc.).

後段文字表示不支援 Big5 的編碼，所以， README.md 在 cmd 下無法使用 more README.md 來讀取並顯示。

[https://zlargon.gitbooks.io/git-tutorial/](https://zlargon.gitbooks.io/git-tutorial/)

## testing command

curl -u "elvishsieh" https://api.github.com/user/repos -d '{"name":"'testing'"}'

error message:
D:\github>curl -u "elvishsieh" https://api.github.com/user/repos -d '{"name":"'testing'"}'
Enter host password for user 'elvishsieh':
{
  "message": "Problems parsing JSON",
  "documentation_url": "https://developer.github.com/v3/repos/#create"
}

curl -X POST -v -u elvishsieh:elvishsieh54 -H "Content-Type: application/json" https://api.bitbucket.org/2.0/repositories/teamsinspace/new-repository4 -d '{"scm": "git", "is_private": "true","fork_policy":"no_public_forks","name":"NewRepo"}'

## Using GraphQL to access github

1 [create github token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)

token is : e84ebba4ae41cbdd2cce9bf254f48b07d54142f4

2. [communicating github GraphQL](https://developer.github.com/v4/guides/forming-calls/#authenticating-with-graphql)

endpoint is [https://api.github.com/graphql](https://api.github.com/graphql) 

curl -i -H "Authorization: bearer e84ebba4ae41cbdd2cce9bf254f48b07d54142f4" -X POST -d "{\"query\": \"query {repository(owner: \"elvishsieh\", name: \"testing\") }\"}" https://api.github.com/graphql

correct command:

curl -H "Authorization: bearer e84ebba4ae41cbdd2cce9bf254f48b07d54142f4" -X POST -d " { \"query\": \"query { viewer { login }}\" } " https://api.github.com/graphql

https://dev-blog.apollodata.com/4-simple-ways-to-call-a-graphql-api-a6807bcdb355

EaseUS® Data Recovery Wizard recovery my delete datas on testing directory.