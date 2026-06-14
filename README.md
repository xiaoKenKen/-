# Unreal & Wwise 音频设计实践说明文档

## 项目概述

本项目基于 Unreal Engine 引擎和 Wwise 音频中间件，完成了空间音频、基础环境声、物件3D音效以及角色脚步声等音频设计模块的实践。项目实现了室内外空间音频效果、环境声循环播放、篝火物件音效以及角色跑步脚步声的完整音频系统。

## 开发环境设置

### 软件环境

- Unreal Engine 5
- Wwise 2024.1.14版本
- GitHub 版本控制

### 环境配置过程

在环境配置过程中，我首先安装了Unreal Engine和Wwise中间件，并完成了两者的整合配置。通过创建GitHub仓库，实现了开发过程中的版本控制和代码管理，确保了开发过程的可追溯性。

## Wwise 音频中间件实现

<img width="493" height="1015" alt="Audio" src="https://github.com/user-attachments/assets/840a71bf-92de-4790-a77b-97d5ef1d8769" />

### 环境声基底资产

创建了可循环播放的环境声资产，配置了3D Positioning设置和自定义的Attenuation衰减曲线，实现了室外环境声的持续播放效果。

### 篝火物件声音资产

构建了包含Random和Blender Container层级结构的篝火音效，通过多层音效叠加实现了更丰富的燃烧声效果，并配置了相应的3D定位和衰减参数。

### 角色跑步声音资产

实现了Game Sync Switch系统，创建了包含两种鞋子类型和四种材质类型（Dirt、Rock、Wood、Grass）的Switch Container嵌套结构，实现了基于材质类型的脚步声切换。

### 空间混响效果

创建了用于模拟空间混响的Aux Bus，配置了Effect插件和3D Positioning设置，实现了声音传送到混响总线的效果。

## Unreal Engine 引擎实现

### 场景空间设计

利用UE自带场景，通过中间和四周的高台模拟不同地面材质，并在一边隔离出大房间来实现室内空间效果。房间内放置了篝火方块和音乐播放角落，形成了完整的室内外空间结构。

### Room和Portal系统

使用Room和Portal对象创建了室内外空间联通，配置了各个Component的功能参数，实现了室内外空间的音频过渡效果。

### 篝火物件实现

通过方块创建了篝火物件，放置在室内空间中，确保了音效的正确播放和混响效果。

### 角色脚步系统
<img width="1961" height="515" alt="fs_bp" src="https://github.com/user-attachments/assets/bd407401-ef71-4134-b223-339c24750887" />
<img width="1292" height="755" alt="fs" src="https://github.com/user-attachments/assets/2379eea9-157e-4ed2-abfe-41b5135410bc" />
<img width="1273" height="336" alt="BP" src="https://github.com/user-attachments/assets/06823195-5c0f-4e64-a282-b95bc765f285" />
将角色跑步声资产以Notify形式配置在角色动画中，并指定到对应的Socket上。创建了四种Physical Material和Surface Type，将材质正确配置到场景中，并对Notify功能进行了改造，实现了Raycast射线检测材质的功能。

## 整体表现

### 场景设计
<img width="1524" height="1146" alt="room_scene" src="https://github.com/user-attachments/assets/daf46fef-b8b0-47f0-a412-dc7e809bcdfc" />
<img width="1571" height="1212" alt="scene" src="https://github.com/user-attachments/assets/0aa917af-3e55-40e4-9a45-09913e28db66" />

基于UE自带场景进行了改造设计，利用高台地形模拟不同材质区域，通过空间隔离创建了具有明显区别的室内外环境，能够充分展示各项音频设计效果。

### 音频效果调整

对各种声音的响度比例进行了细致调整，确保整体听感舒适，最终响度范围控制在-27至-40 LUFS之间。

## 开发过程中的想法与问题

### 技术选型思考

在项目开始阶段，我选择利用UE自带场景进行改造，这样可以更专注于音频系统的设计实现，而不是场景建模。通过高台地形模拟不同材质区域的设计，既简化了场景制作，又能够有效展示音频效果。

### 遇到的主要问题

1. **版本兼容性问题**
老师视频教程推荐使用Wwise 2024.1.2版本，但在实际使用中发现该版本已不支持与UE进行文件传输连接。经过尝试后，不得不更换为2024.1.14版本，这个过程花费了一些时间进行环境重新配置。
2. **材质音效映射错误**
在导入wood和rock音效后，发现在UE环境中两者都播放rock的声音。通过从Wwise环节开始逐步排查，最终发现是UE中两个材质都错误地连接了rock的声音，这个调试过程较为耗时。
3. **混响效果调试困难**
在房间中添加了背景音乐以模拟高混响环境，但在Wwise中调整曲线时，始终无法达到教程中展示的混响效果。尝试了多种参数组合，但效果变化不显著，怀疑可能是音源本身的问题，这个问题在项目结束时仍未完全解决。

## 项目总结

通过本次实践项目，深入理解了Unreal Engine与Wwise中间件的整合工作流程，掌握了空间音频、环境声设计、物件音效和角色脚步声等核心音频设计技术。虽然在开发过程中遇到了一些技术挑战，但通过问题排查和解决方案的寻找，获得了宝贵的实践经验。

项目最终实现了预期的音频设计效果，包括室内外空间音频过渡、环境声循环播放、篝火物件音效以及基于材质类型的动态脚步声系统。通过GitHub版本控制，确保了开发过程的规范性和可追溯性。

