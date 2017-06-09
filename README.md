<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orga6d049b">1. Learn Git 笔记</a>
<ul>
<li><a href="#orgd3fa561">1.1. git rebase -i 代码修改</a></li>
<li><a href="#org1fcee2d">1.2. git commit &#x2013;amend 后,vim编辑提交后,出现错误:vi error &#x2026;</a></li>
<li><a href="#orgf0874c1">1.3. 单独恢复一个文件到指定的版本</a></li>
<li><a href="#orgda6bbd3">1.4. 解决没有共同祖先的分支时错误：fatal: refusing to merge unrelated histories</a></li>
<li><a href="#orge385a89">1.5. 更改 服务器端 origin</a></li>
</ul>
</li>
</ul>
</div>
</div>

<a id="orga6d049b"></a>

# Learn Git 笔记


<a id="orgd3fa561"></a>

## git rebase -i 代码修改

    $ git log 
     looking for the hash number your want to back to , then 'git rebase -i fhslfjs26482482' , 
     fhslfjs26482482 is previous hashnum than you want modify one.
    $ git rebase -i "fhslfjs26482482"
    
     pick bdccbef Create README.md & add branchDec. hehe                                                  
     pick 4a121e1 modify by git rebase, hehe                                                              
     edit 9baf6e1 add a new file, --amend                                                                 
     pick e559e59 I add commit --amend , vi error solved 
    
    修改完成后 , git rebase --continue

注意: 多人协作,共同开发时,不要对master分支rebase, 不然, 你的队友会骂娘的.  
      本地  **git checkout -b newbranch** 只对 newbranch进行 rebase, 完成后 **merge** 到本地的 **master** 分支,再 **push** 到 服务器端.


<a id="org1fcee2d"></a>

## git commit &#x2013;amend 后,vim编辑提交后,出现错误:vi error &#x2026;

    $ git config --global core.editor "/usr/bin/vim --noplugin"
    修改为vim 编辑器


<a id="orgf0874c1"></a>

## 单独恢复一个文件到指定的版本

    首先查看该文件的历史版本信息：git log Default@2x.png
    
    记录下需要恢复的commit版本号：如 9aa51d89799716aa68cff3f30c26f8815408e926
    
    恢复该文件：git reset 9aa51d89799716aa68cff3f30c26f8815408e926 Default@2x.png
    
    提交git:git commit -m "revert old file"


<a id="orgda6bbd3"></a>

## 解决没有共同祖先的分支时错误：fatal: refusing to merge unrelated histories

    先把github上的版本pull 下来
    $:git pull origin master --allow-unrelated-histories
    合并后再push上remote。


<a id="orge385a89"></a>

## 更改 服务器端 origin

    $git remote rm origin  
    $git remote add origin git@github.com:username/myapp.git

