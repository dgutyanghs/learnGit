
# Table of Contents

1.  [Learn Git 笔记](#org4730c00)
    1.  [git rebase -i 代码修改](#orga9b1816)
    2.  [git commit &#x2013;amend 后,vim编辑提交后,出现错误:vi error &#x2026;](#org8c5ddff)
    3.  [单独恢复一个文件到指定的版本](#orgb7723a8)
    4.  [解决没有共同祖先的分支时错误：fatal: refusing to merge unrelated histories](#org8050533)
    5.  [更改 服务器端 origin](#org75c38b2)
    6.  [文件移出缓冲区rm &#x2013;cached](#org93df602)
    7.  [使用Gitlab一键安装包后的日常备份恢复与迁移](#orgf79ad19)
        1.  [本文转自：](#org75ffe92)
    8.  [Git archive 导出zip包](#orgd6df44a)


<a id="org4730c00"></a>

# Learn Git 笔记


<a id="orga9b1816"></a>

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


<a id="org8c5ddff"></a>

## git commit &#x2013;amend 后,vim编辑提交后,出现错误:vi error &#x2026;

    
    $ git config --global core.editor "/usr/bin/vim --noplugin"
    修改为vim 编辑器


<a id="orgb7723a8"></a>

## 单独恢复一个文件到指定的版本

    首先查看该文件的历史版本信息：git log Default@2x.png
    
    记录下需要恢复的commit版本号：如 9aa51d89799716aa68cff3f30c26f8815408e926
    
    恢复该文件：git reset 9aa51d89799716aa68cff3f30c26f8815408e926 Default@2x.png
    
    提交git:git commit -m "revert old file"


<a id="org8050533"></a>

## 解决没有共同祖先的分支时错误：fatal: refusing to merge unrelated histories

    先把github上的版本pull 下来
    $:git pull origin master --allow-unrelated-histories
    合并后再push上remote。


<a id="org75c38b2"></a>

## 更改 服务器端 origin

    $git remote rm origin  
    $git remote add origin git@github.com:username/myapp.git 


<a id="org93df602"></a>

## 文件移出缓冲区rm &#x2013;cached

    git add file.txt
    git rm --cached file.txt
    将file.txt 从cached中移除


<a id="orgf79ad19"></a>

## 使用Gitlab一键安装包后的日常备份恢复与迁移


<a id="org75ffe92"></a>

### 本文转自：<https://segmentfault.com/a/1190000002439923>

    Gitlab 创建备份
    使用Gitlab一键安装包安装Gitlab非常简单, 同样的备份恢复与迁移也非常简单. 使用一条命令即可创建完整的Gitlab备份:
    
    gitlab-rake gitlab:backup:create
    使用以上命令会在/var/opt/gitlab/backups目录下创建一个名称类似为1393513186_gitlab_backup.tar的压缩包, 这个压缩包就是Gitlab整个的完整部分, 其中开头的1393513186是备份创建的日期.
    
    Gitlab 修改备份文件默认目录
    你也可以通过修改/etc/gitlab/gitlab.rb来修改默认存放备份文件的目录:
    
    gitlab_rails['backup_path'] = '/mnt/backups'
    /mnt/backups修改为你想存放备份的目录即可, 修改完成之后使用gitlab-ctl reconfigure命令重载配置文件即可.
    
    Gitlab 自动备份
    也可以通过crontab使用备份命令实现自动备份:
    
    sudo su -
    crontab -e
    加入以下, 实现每天凌晨2点进行一次自动备份:
    
    0 2 * * * /opt/gitlab/bin/gitlab-rake gitlab:backup:create
    Gitlab 恢复
    同样, Gitlab的从备份恢复也非常简单:
    
    # 停止相关数据连接服务
    gitlab-ctl stop unicorn
    gitlab-ctl stop sidekiq
    
    # 从1393513186编号备份中恢复
    gitlab-rake gitlab:backup:restore BACKUP=1393513186
    
    # 启动Gitlab
    sudo gitlab-ctl start
    Gitlab迁移
    迁移如同备份与恢复的步骤一样, 只需要将老服务器/var/opt/gitlab/backups目录下的备份文件拷贝到新服务器上的/var/opt/gitlab/backups即可(如果你没修改过默认备份目录的话). 但是需要注意的是新服务器上的Gitlab的版本必须与创建备份时的Gitlab版本号相同. 比如新服务器安装的是最新的7.60版本的Gitlab, 那么迁移之前, 最好将老服务器的Gitlab 升级为7.60在进行备份.
    
    其他
    最新版本的Gitlab已经修复了HTTPS设备的BUG, 现在使用官方HTTPS配置即可轻松启用HTTPS.  


<a id="orgd6df44a"></a>

## Git archive 导出zip包

    git archive -o latest.zip HEAD
    git archive -o latest.zip master

