# Test Internet Speed

You can use the Speedtest CLI application on Linux, Ubuntu, or Debian-based distributions. This is a tool provided by Ookla to test your internet speed from the command line. Note: Speedtest CLI is also available on many different operating systems, and the installation command may vary depending on the operating system you are using. In case you are using a different operating system, refer to the [Speedtest CLI](https://www.speedtest.net/apps/cli) documentation for installation and usage instructions for your operating system.

### To test your internet speed using Speedtest CLI on Linux <a href="#kiemtratocdointernet-kiemtratocdointernetbangspeedtestclitrenhedieuhanhlinux" id="kiemtratocdointernet-kiemtratocdointernetbangspeedtestclitrenhedieuhanhlinux"></a>

Follow these steps to install and use Speedtest CLI:

1. Open a terminal window.
2.  Run the following command to download and install:

    | `curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.rpm.sh \| sudo bash` |
    | ----------------------------------------------------------------------------------------------------- |

    Note that this command will require administrative privileges, so you'll need to enter the administrator password to proceed.
3.  After the installation process is complete, run the following command to install Speedtest CLI:<br>

    | `sudo yum install speedtest` |
    | ---------------------------- |
4.  Once the installation process is complete, you can perform an internet speed test by running the following command:

    | `speedtest` |
    | ----------- |

    Speedtest CLI will automatically find the nearest server to perform the test and then display the results of download and upload speeds as well as latency.\
    <br>

    \
    <br>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766895/image2023-8-9_13-9-55.png?version=1&#x26;modificationDate=1691561396000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
5.  However, after 3 days, the speed will decrease to Download: 220.46 Mbps/s and Upload: 262.51 Mbps/s as shown below:\
    <br>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766895/image2023-8-30_15-11-56.png?version=1&#x26;modificationDate=1693383117000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### To test your internet speed using Speedtest CLI on Ubuntu: <a href="#kiemtratocdointernet-kiemtratocdointernetbangspeedtestclitrenhedieuhanhunbutu" id="kiemtratocdointernet-kiemtratocdointernetbangspeedtestclitrenhedieuhanhunbutu"></a>

Follow these steps to install and use Speedtest CLI:

1. Open a terminal window.
2.  Run the following command to download and install:

    | `sudo apt-get install curlcurl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.deb.sh \| sudo bash` |
    | ------------------------------------------------------------------------------------------------------------------------------ |

    Note that this command will require administrative privileges, so you'll need to enter the administrator password to proceed.
3.  After the installation process is complete, run the following command to install Speedtest CLI:<br>

    | `sudo apt-get install speedtest` |
    | -------------------------------- |
4.  Once the installation process is complete, you can perform an internet speed test by running the following command:

    | `speedtest` |
    | ----------- |

    Speedtest CLI will automatically find the nearest server to perform the test and then display the results of download and upload speeds as well as latency.\
    <br>



    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766895/image2023-8-4_14-38-16.png?version=1&#x26;modificationDate=1691134696000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### Internet Speed Test with Fast <a href="#kiemtratocdointernet-kiemtratocdointernetbangfast" id="kiemtratocdointernet-kiemtratocdointernetbangfast"></a>

In addition to Speedtest CLI, you can also use Fast. Fast is an open-source CLI utility developed by Netflix's fast.com service, and you can also access it directly from your browser.

Fast is a perfect tool for those who just want to check download speed in a very simple way.

1.  To use it via the command line, you'll need to properly install npm on your system and then run the command:

    | `sudo npm install --global fast-cli` |
    | ------------------------------------ |
2.  You can also install it via snap:

    | `sudo snap install fast` |
    | ------------------------ |
3.  After installation, you can run it via the command line:

    | `fast` |
    | ------ |



    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766895/image2023-8-9_10-11-3.png?version=1&#x26;modificationDate=1691550664000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### Monitoring Internet Speed with vMonitor on the dashboard <a href="#kiemtratocdointernet-giamsattocdointernetbangvmonitortrenbangdieukhien" id="kiemtratocdointernet-giamsattocdointernetbangvmonitortrenbangdieukhien"></a>

* You can access the vMonitor homepage at: [https://hcm-3.console.greennode.ai/vmonitor/dashboard](https://hcm-3.console.greennode.ai/vmonitor/dashboard) to monitor the internet speed of your server.<br>

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766895/image2023-8-14_15-24-20.png?version=1&#x26;modificationDate=1692001461000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### SpeedTest International Location

&#x20;

| Country                 | City        | Provider               | Host                                                           | ID     | CLI                 | Status updated 30-Oct-2024 |
| ----------------------- | ----------- | ---------------------- | -------------------------------------------------------------- | ------ | ------------------- | -------------------------- |
| Republic of Singapore   | Singapore   | MyRepublic             | speedtest.myrepublic.com.sg:8080                               | 5935   | speedtest -s 5935   | Activate                   |
| Republic of Singapore   | Singapore   | NewMedia Express       | [www.speedtest.com.sg:8080](https://www.speedtest.com.sg:8080) | 367    | speedtest -s 367    | Activate                   |
| Republic of Singapore   | Singapore   | PT FirstMedia          | sg-speedtest.fast.net.id:8080                                  | 7556   | speedtest -s 7556   | Activate                   |
| Republic of Singapore   | Singapore   | StarHub Mobile Pte Ltd | co2speedtest1.starhub.com:8080                                 | 4235   | speedtest -s 4235   | Activate                   |
| Singapore               | Singapore   | Singtel                | speedtest.singnet.com.sg:8080                                  | 13623  | speedtest -s 13623  | Activate                   |
| Republic of Singapore   | Singapore   | Viewqwest Pte Ltd      | speedtest10.vqbn.com:8080                                      | 2054   | speedtest -s 2054   | Activate                   |
| _Republic of Singapore_ | _Singapore_ | _M1 Limited_           | _m1speedtest1.m1net.com.sg:8080_                               | _7311_ | _speedtest -s 7311_ | _Activate_                 |

&#x20;

