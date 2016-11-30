<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgheadline4">1. Learn Git 笔记</a>
<ul>
<li><a href="#orgheadline1">1.1. git rebase -i 代码修改</a></li>
<li><a href="#orgheadline2">1.2. git commit &#x2013;amend 后,vim编辑提交后,出现错误:vi error &#x2026;</a></li>
<li><a href="#orgheadline3">1.3. 单独恢复一个文件到指定的版本</a></li>
</ul>
</li>
</ul>
</div>
</div>

# Learn Git 笔记<a id="orgheadline4"></a>

## git rebase -i 代码修改<a id="orgheadline1"></a>

    $ git log 
     looking for the hash number your want to back to , then 'git rebase -i fhslfjs26482482' , 
     fhslfjs26482482 is previous hashnum than you want modify one.
    $ git rebase -i "fhslfjs26482482"
    
     pick bdccbef Create README.md & add branchDec. hehe                                                  
     pick 4a121e1 modify by git rebase, hehe                                                              
     edit 9baf6e1 add a new file, --amend                                                                 
     pick e559e59 I add commit --amend , vi error solved 
    
    修改完成后 , git rebase --continue

## git commit &#x2013;amend 后,vim编辑提交后,出现错误:vi error &#x2026;<a id="orgheadline2"></a>

    $ git config --global core.editor "/usr/bin/vim --noplugin"
    修改为vim 编辑器

## 单独恢复一个文件到指定的版本<a id="orgheadline3"></a>

    首先查看该文件的历史版本信息：git log Default@2x.png
    
    记录下需要恢复的commit版本号：如 9aa51d89799716aa68cff3f30c26f8815408e926
    
    恢复该文件：git reset 9aa51d89799716aa68cff3f30c26f8815408e926 Default@2x.png
    
    提交git:git commit -m "revert old file"
