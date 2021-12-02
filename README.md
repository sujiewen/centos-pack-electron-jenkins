# centos-pack-electron-jenkins
jenkins electron centos
用centos 直接把electron打成exe文件，无法成功或者有其它问题，我后面在网友帮助下，在docker下打包electron很流畅。由于我要配合jenkins自动打包，这里走了一些弯路，最终使用下面方案打包
做下备份，第一次使用docker， 不会。。。。。



1，请先安装jenkins和docker

2，运行docker， 并把工程目录引射到docker里面，看命令：
    
docker run -d --rm -it --env-file <(env | grep -iE 'DEBUG|NODE_|ELECTRON_|YARN_|NPM_|CI|CIRCLE|TRAVIS_TAG|TRAVIS|TRAVIS_REPO_|TRAVIS_BUILD_|TRAVIS_BRANCH|TRAVIS_PULL_REQUEST_|APPVEYOR_|CSC_|GH_|GITHUB_|BT_|AWS_|STRIP|BUILD_') --env ELECTRON_CACHE="/root/.cache/electron" --env ELECTRON_BUILDER_CACHE="/root/.cache/electron-builder" --env ELECTRON_MIRROR="http://npm.taobao.org/mirrors/electron/" --env ELECTRON_BUILDER_BINARIES_MIRROR="http://npm.taobao.org/mirrors/electron-builder-binaries/" -v /home/jenkins/PC:/project -v /home/jenkins/PC/node_modules:/project/node_modules -v ~/.cache/electron:/root/.cache/electron -v ~/.cache/electron-builder:/root/.cache/electron-builder electronuserland/builder:wine
3，在jenkins 配置shell( -i docker run id):

docker exec  -i 80829739a658 bash -c 'NODE_ENV=production && npm install --arch=x64 --platform=win32 && SHARP_IGNORE_GLOBAL_LIBVIPS=1  && npm install --arch=x64 --platform=win32 sharp && npm install electron-builder@22.11.5 -D && npm install electron@^12.0.16 -D  && npm install electron-devtools-installer@^3.1.0 -D && npm install electron-rebuild@^2.3.5 -D && npm install vue-cli-plugin-electron-builder@~2.0.0 -D && npm install vue-cli-plugin-electron-builder@~2.0.0 -D && npm install electron-is@^3.0.0 && npm install electron-is-dev@^0.3.0 && npm install electron-log@^4.3.2 && npm install electron-packager@^15.2.0 && npm install electron-updater@^4.3.5 && npm install electron-find-in-page@^1.0.8 && ./node_modules/.bin/vue-cli-service electron:build --mode lc --windows --x64'
w_path="/xx/xx/dist_electron"
if [ ! -d ${w_path} ]; then
mkdir ${w_path}
else 
mv ${w_path} ${w_path}_$(date +%Y%m%d-%H%M%S)
mkdir ${w_path}
fi
。。。。。。。
