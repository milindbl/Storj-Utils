[![License](https://img.shields.io/github/license/AntonMZ/Storj-Utils.svg)](https://github.com/AntonMZ/Storj-Utils/blob/master/LICENSE)

**Compatible with Stat Storj Statistics (https://stat.storj.maxrival.com)**

**Compatible with storjshare daemon: 4.0.1, core: 7.0.0, protocol: 1.2.0**

# Storj-Utils
This is a fork of AntonMZ's https://github.com/AntonMZ/Storj-Utils repo modified to make it work using a Alpine Linux 3.4 Docker instance running within a Synology NAS. This is a script for checking the basic parameters of the Storjshare-Cli node.<br/>

![Storj bash health script](http://maxrival.com/content/images/2017/05/storj-bash-healt-script-v1.0.2.png)

## Installation and configuration
Installation of required components
```
apk add git
apk add jq
apk add net-tools
apk add bc
apk add curl
apk add ncurses
apk add util-linux
```

You need to configure the [config.cfg](config.cfg) configuration file and then run the script periodically sending statistics to [https://stat.storj.maxrival.com](https://stat.storj.maxrival.com/):
1. Clone project
```
git clone https://github.com/milindbl/Storj-Utils
```
2. Edit the configuration file [config.cfg](config.cfg)
```
LOGS_FOLDER=/root/.config/storjshare/logs
CONFIGS_FOLDER=/root/.config/storjshare/configs
WATCHDOG_LOG=/var/log/storjshare-daemon-status.log
EMAIL=az@maxrival.com
```
Where:
* LOGS_FOLDER – StorjShare logs folder;
* CONFIGS_FOLDER – where your configuration folder is located;
* WATCHDOG_LOG – obsolete;
* EMAIL – used to authorize the [website statistics](https://stat.storj.maxrival.com/).
3. Run the script.
```
./health.sh
```
or
```
sudo su -l USER -c "health.sh"
```

4. Periodically run script

Using crontab
```
crontab -e
*/5 * * * * /bin/bash /PATH_TO_SCRIPT/health.sh --api > /dev/null 2>&1
```
or

using scheduled task in Synology (Task Scheduler -> Create -> Scheduled Task -> User-defined script) and enter this run command
```
sudo docker exec NAME_OF_DOCKER_CONTAINER bash /PATH_TO_SCRIPT/health.sh --api > /dev/null 2>&1
```

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
