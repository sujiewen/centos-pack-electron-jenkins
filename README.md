# centos-pack-electron-jenkins
jenkins electron centos
用centos 直接把electron打成exe文件，无法成功或者有其它问题，我后面在网友帮助下，在docker下打包electron很流畅。由于我要配合jenkins自动打包，这里走了一些弯路，最终使用下面方案打包



1，请先安装jenkins和docker
2，运行docker:
    
docker run -d --rm -it --env-file <(env | grep -iE 'DEBUG|NODE_|ELECTRON_|YARN_|NPM_|CI|CIRCLE|TRAVIS_TAG|TRAVIS|TRAVIS_REPO_|TRAVIS_BUILD_|TRAVIS_BRANCH|TRAVIS_PULL_REQUEST_|APPVEYOR_|CSC_|GH_|GITHUB_|BT_|AWS_|STRIP|BUILD_') --env ELECTRON_CACHE="/root/.cache/electron" --env ELECTRON_BUILDER_CACHE="/root/.cache/electron-builder" --env ELECTRON_MIRROR="http://npm.taobao.org/mirrors/electron/" --env ELECTRON_BUILDER_BINARIES_MIRROR="http://npm.taobao.org/mirrors/electron-builder-binaries/" -v /home/jenkins/warehousePC:/project -v /home/jenkins/warehousePC/node_modules:/project/node_modules -v ~/.cache/electron:/root/.cache/electron -v ~/.cache/electron-builder:/root/.cache/electron-builder electronuserland/builder:wine
