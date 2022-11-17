## 设置淘宝源
npm config set registry https://registry.npm.taobao.org

## 查看源，可以看到设置过的所有的源
npm config get registry

## 本次从淘宝仓库源下载
npm --registry=https://registry.npm.taobao.org install

---

## 设置特定源
npm config set registry http://npm.特定源.com/

## 需要对特定源进行登录
npm adduser --registry http://npm.特定源.com/