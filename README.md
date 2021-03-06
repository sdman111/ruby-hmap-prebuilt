# ruby-hmap-prebuilt
结合 [hmap](https://github.com/milend/hmap) 与 [cocoapods-hmap](https://github.com/Cat1237/cocoapods-hmap) 结合, 将 cocoapods 插件脚本化, 可用于构建机等可能不能安装插件的环境



## Usuage

1. 将 `hmap-prebuilt` 目录移动到工程主目录 (与 `Pods` 目录同级)
3. `Podfile` 引入 `hmap-prebuilt.rb`
4. 在 `post_install` 中调用 `hmap_prebuilt` 函数并传入 `installer` 参数

![image-20210926220940705](https://gitee.com/wuzhiying1/image-bed/raw/master/image-20210926220940705.png)



## Need to know

脚本依赖 `post_install` 的上下文，用于遍历头文件，所以必须传入 `installer` 参数；假如需要摆脱 `post_install` 的上下文依赖，可以选择单独遍历 `Pods` 目录生成下图格式的 `json` 文件，再传给 `HMapSaver` 进行处理

![image-20210926221453027](https://gitee.com/wuzhiying1/image-bed/raw/master/image-20210926221453027.png)



## Problems

1. Json convert to Hmap转换时间过长。2.4MB大小的 json 传给 HMapSaver 生成 Hmap需要的处理时间长达 30+秒（补充：cocoapods-hmap更新后生成速度大幅提升）
2. 通过 header_mappings_by_file_accessor 获取的头文件不够足以覆盖工程中全部头文件的引用，需要筛选 target 使用



## Todo

1. json or hmap 增量更新 （need to learn）



## Thanks

感谢 [hmap](https://github.com/milend/hmap) ，[cocoapods-hmap](https://github.com/Cat1237/cocoapods-hmap) 两位大佬的开源，特别感谢后者将生成 hmap 和转换 hmap 的 ruby 代码开源，使得脚本可以摆脱额外的命令行工具安装
