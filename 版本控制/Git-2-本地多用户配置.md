## Git本地多用户配置

场景：一台开发电脑上拥有2个git账户，对不同的仓库使用不同的账户提交。  

步骤一：添加用户
```
# 如果已经存在一个git用户，直接按照ssh命令添加用户即可，如果从来没有配置git用户，新生成2个key即可
ssh-keygen -t rsa -C "user1@gmai.com" -f ~/.ssh/id_rsa_user1
ssh-keygen -t rsa -C "user2@gmai.com" -f ~/.ssh/id_rsa_user2

# 新增 config文件
cd ~/.ssh
vim config

# config配置如下
Host git1
HostName github.com
User user1
IdentityFile ~/.ssh/id_rsa_user1

Host git2
HostName github.com
User user2
IdentityFile ~/.ssh/id_rsa_user2

# 追加秘钥
ssh-add ~/.ssh/id_rsa_user1
ssh-add ~/.ssh/id_rsa_user2

# 将公钥配置进git远程仓库后，即可进行推送，但是有两种情况：

## 情况一：全新的项目，clone的地址应该修改
git clone git@github.com:***/***.git        # 原有地址，应该以下列方式clone
git clone git@user1::***/***..git
# 进入项目后配置
git config --local user.name "user1"
git config --local user.email "user1@gmail.com"

## 情况二：已经存在的项目，进入项目目录：
git config --local user.name "user1"
git config --local user.email "user1@gmail.com"
vim ./git/config                      # 修改项目目录下git配置的push用户
url = git@github.com:***/***.git      # 将本句修改为git@user1:***/***.git

# 此时该项目就会以user1身份进行维护
```
