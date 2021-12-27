<div align="center">
  <p>
    <h1>
      <a href="https://github.com/MiCode/MiBridge">
        <img src="http://f2.market.mi-img.com/download/MiPass/08df2de4d3ab74451b8f86ef86415eaddd122982d/xiaomi_circle.svg" alt="MiBridge" />
      </a>
      <br />
      Flameshot
    </h1>
    <h4>Powerful yet simple to use screenshot software.</h4>
  </p>
  <p>
    <a href="https://github.com/flameshot-org/flameshot/actions?query=workflow%3APackaging%28Linux%29">
      <img src="https://img.shields.io/github/workflow/status/flameshot-org/flameshot/Packaging(Linux)?label=gnu%2Flinux" alt="GNU/Linux Build Status" />
    </a>
    <a href="https://github.com/flameshot-org/flameshot/actions?query=workflow%3APackaging%28Windows%29">
      <img src="https://img.shields.io/github/workflow/status/flameshot-org/flameshot/Packaging(Windows)?label=windows" alt="Windows Build Status" />
    </a>
    <a href="https://github.com/flameshot-org/flameshot/actions?query=workflow%3APackaging%28MacOS%29">
      <img src="https://img.shields.io/github/workflow/status/flameshot-org/flameshot/Packaging(MacOS)?label=macos" alt="MacOS Build Status" />
    </a>
    <a href="https://flameshot.org/nightly">
      <img src="https://img.shields.io/badge/nightly%20builds-available-%23AA00FF" alt="Nightly Build" />
    </a>
    <a href="https://github.com/flameshot-org/flameshot/releases">
      <img src="https://img.shields.io/github/release/flameshot-org/flameshot.svg" alt="Latest Stable Release" />
    </a>
    <a href="https://github.com/flameshot-org/flameshot/releases">
      <img src="https://img.shields.io/github/downloads/flameshot-org/flameshot/total.svg" alt="Total Downloads" />
    </a>
    <a href="https://github.com/flameshot-org/flameshot/blob/master/LICENSE">
      <img src="https://img.shields.io/github/license/flameshot-org/flameshot.svg" alt="License" />
    </a>
  <a href="https://hosted.weblate.org/engage/flameshot/">
    <img src="https://hosted.weblate.org/widgets/flameshot/-/flameshot/svg-badge.svg" alt="Translation status" />
  </a>
  <a href="https://flameshot.org">
      <img src="https://img.shields.io/github/release/flameshot-org/flameshot.svg?label=docs" alt="Docs" />
    </a>
    <br>
    <a href="https://snapcraft.io/flameshot">
      <img alt="Get it from the Snap Store" src="https://snapcraft.io/static/images/badges/en/snap-store-black.svg" />
    </a>
    <a href="https://flathub.org/apps/details/org.flameshot.Flameshot">
      <img height="60" alt="Download on Flathub" src="https://flathub.org/assets/badges/flathub-badge-en.svg"/>
    </a>
  </p>
</div>


# 小米应用加速器
## 其他语言
[English](./README.md)


## Index

- [我们的目的](#我们的目的)
- [简介](#简介)
- [我们的优势](#我们的优势)
- [接入说明](#接入说明)
  - [申请调试权限](#申请调试权限)
  - [接口定义](#接口定义)
  - [申请正式权限](#申请正式权限)
  - [更多合作](#更多合作)




## 我们的目的
一切为了用户，让用户得到最好的体验！
## 简介
小米应用加速器向开发者提供申请系统资源的接口，可以为开发者提升应用关键场景下的性能，提升用户使用体验。
## 我们的优势
* __*轻量级接入*__<br>
  通过JAR包接入，大小只有几kb, 不会对开发者的应用造成负担
* __*快速系统通信*__<br>
  通过Binder直接与系统层进行通信，申请系统资源，快速高效
* __*场景化定制*__<br>
  为开发者在不同的场景下提供不同级别的系统资源
## 接入说明<br>
*MiBridge.jar*<br>
&emsp;您可以引入此jar包调用小米应用加速器相关接口。<br>
*TestMiBridge*<br>
&emsp;此目录包含： <br>
&emsp;&emsp;*mibridge*: MiBridge jar包的实现代码。<br>
&emsp;&emsp;*app*: 测试MiBridge的app代码。<br>
#### 申请调试权限
请提供以下信息，发送到邮箱xiaomi-mispeed-support@xiaomi.com, 申请接入调试权限。<br>
#### 邮件主题：xx（APP名称）申请小米应用加速器接入调试权限<br>

应用包名 | 申请人 |
---- | ----- |
com.mi.testmibridge | 张三 |

我们将会为您开通调试权限．

[__支持设备版本列表__](./support_devices.md)

#### 2. 接口定义
__权限检查接口__<br>

1. ```boolean checkPermission(String pkg, int uid)```<br>
      __介绍：检查应用是否有权限__<br>

      参数：<br>
      *pkg* : 应用包名<br>
      *uid* : android.os.Process.myUid()<br>

      返回结果：<br>
      true: 权限检查通过<br>
      false: 权限检查失败，无接口使用权限<br>

__系统资源申请接口__<br>

2. ```int requestCpuHighFreq(int uid, int level, int timeoutms)```<br>
      __介绍：向系统申请cpu频率资源的接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>
      *level* : 需要的cpu频率level，系统将会根据不同机型设置不同的cpu频率<br>
      *timeoutms* : 申请cpu资源的持续时间<br>

      Level级别 | 解释（以小米8为例）| timeoutms
      ---- | -----|-----
      1 | Level 1 将会设置系统当前最小频率为系统最高频率 |  最长10s
      2 | Level 2 将会设置系统当前最小频率为系统较高频率<br>例：小米8对应大核最低2.2GHz, 小核最低1.5GHz |  最长5s
      3 | Level 3 将会设置系统当前最小频率为系统正常频率以上<br>例：小米8对应大核最低1.9GHz, 小核最低1.0GHz |  最长1.5s

      __注意：请谨慎使用Level 1级别。Level 1级别使用场景数量限制为5，__<br>
      __Level 2级别使用场景数量限制为20，Level 3 不做限制。__<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

3. ```int cancelCpuHighFreq(int uid)```<br>
      __介绍：取消申请cpu频率资源的接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

4. ```int requestThreadPriority(int uid, int req_tid, int timeoutms)```<br>
      __介绍：申请线程获得高优先级，将会优先得到调度运行__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>
      *req_tid* : 申请的线程id<br>
      *timeoutms* : 申请的时长<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

5. ```int cancelThreadPriority (int uid, int req_tid)```<br>
      __介绍：取消申请线程优先级的接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>
      *req_tid* : 取消的线程id<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

6. ```int requestGpuHighFreq(int uid, int level, int timeoutms)```<br>
      __介绍：向系统申请gpu频率资源的接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>
      *level* : 需要的gpu频率level，系统将会根据不同机型设置不同的gpu频率<br>
      *timeoutms* : 申请gpu资源的持续时间<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

7. ```int cancelGpuHighFreq(int uid)```<br>
      __介绍：取消申请gpu频率资源的接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>

      返回结果：<br>
       0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

8. ```int requestDdrHighFreq(int uid, int level, int timeoutms)```<br>
      __介绍：向系统申请ddr频率资源的接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>
      *level* : 需要的ddr频率level，系统将会根据不同机型设置不同的ddr频率<br>
      *timeoutms* : 申请ddr资源的持续时间<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

9. ```int cancelDdrHighFreq(int uid)```<br>
      __介绍：取消申请ddr频率资源的接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>

      返回结果：<br>
       0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

10. ```int requestIOPrefetch(int uid, String filePath)```<br>
      __介绍：申请IO预读取接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>
      *filePath* : 预读取的文件路径<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

11. ```int requestBindCore(int uid, int req_tid)```<br>
      __介绍：申请线程优先大核运行接口__<br>

      参数：<br>
      *uid* : android.os.Process.myUid()<br>
      *req_tid* : 申请的线程id<br>

      返回结果：<br>
      0:   Success<br>
      -1:  Fail<br>
      -2:  Permission not granted!<br>

<h4 id="formal">3. 申请正式权限</h4>
请提供以下信息，发送到邮箱xiaomi-mispeed-support@xiaomi.com, 申请正式权限。<br>
邮件主题：xx（APP名称）申请小米应用加速器正式权限<br>
__1. 资源接口使用场景<br>

场景 | cpu level | thread priority | timeout (ms)
---- | ----- | ------ | -------
打开xxx页面 | 1 | 0 | 100
Xxx滑动 | 2 | 0 | 1000
场景3 | 3 | 1 | 500
场景4 | 1 | 0 | 100
场景5 | 0 | 1 |2000

__2. 性能测试<br>

场景 | 具体测试内容 | 优化前 | 优化后 | 提升
---- | ----- | ------ | ------- | --------
进入某页面 | 进入页面耗时 | 100 ms | 80 ms | 20%
某页面滑动 | 滑动丢帧数(率) | 10% | 6% | 40%
场景3 | 测试内容3 | .. | .. |..

备注：我们也会根据您提供的场景进行性能测试。<br>

__3. 功耗测试<br>

场景 | Base | 接入后 | Diff
---- | ----- | ------ | -------
场景1 | 1000 mA | 1050 mA | 50
场景2 | .. | .. | ..

备注：我们也会根据您提供的场景进行功耗测试。<br>


#### 4. 更多合作
后续将会开放更多接口<br>
requestIOHighFreq，requestMemory，requestNetwork等

后续可以提供的支持<br>
为您的应用提供更多的支持（例如，卡顿打点，内存泄漏打点），提升应用的性能，提升用户的使用满意度。

<table>
  <tr>
    <th>Host Type</th>
    <th>Toolchain</th>
    <th>Branch</th>
    <th>Build Status</th>
    <th>Test Status</th>
    <th>Code Coverage</th>
  </tr>
  <tr>
    <td>Windows</td>
    <td>VS2019</td>
    <td>master</td>
    <td>
      <a  href="https://dev.azure.com/tianocore/edk2-ci/_build/latest?definitionId=32&branchName=master">
      <img src="https://dev.azure.com/tianocore/edk2-ci/_apis/build/status/Windows%20VS2019%20CI?branchName=master"/></a>
    </td>
    <td>
      <a  href="https://dev.azure.com/tianocore/edk2-ci/_build/latest?definitionId=32&branchName=master">
      <img src="https://img.shields.io/azure-devops/tests/tianocore/edk2-ci/32.svg"/></a>
    </td>
    <td>
      <a  href="https://dev.azure.com/tianocore/edk2-ci/_build/latest?definitionId=32&branchName=master">
      <img src="https://img.shields.io/badge/coverage-coming_soon-blue"/></a>
    </td>
  </tr>
  <tr>
    <td>Ubuntu</td>
    <td>GCC</td>
    <td>master</td>
    <td>
      <a  href="https://dev.azure.com/tianocore/edk2-ci/_build/latest?definitionId=31&branchName=master">
      <img src="https://dev.azure.com/tianocore/edk2-ci/_apis/build/status/Ubuntu%20GCC5%20CI?branchName=master"/></a>
    </td>
    <td>
      <a  href="https://dev.azure.com/tianocore/edk2-ci/_build/latest?definitionId=31&branchName=master">
      <img src="https://img.shields.io/azure-devops/tests/tianocore/edk2-ci/31.svg"/></a>
    </td>
    <td>
      <a  href="https://dev.azure.com/tianocore/edk2-ci/_build/latest?definitionId=31&branchName=master">
      <img src="https://img.shields.io/badge/coverage-coming_soon-blue"/></a>
    </td>
  </tr>
</table>
