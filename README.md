# centos-yum-security

Since the `yum --security` plugin does not work on CentOS, 
this is a workaround for installing/querying security updates on CentOS 7.

Built around `centos-package-cron`:
https://github.com/wied03/centos-package-cron

## Usage and license(s):
```
centos-yum-security [-d] [-h] [-y]

Emulate the yum --security plugin for CentOS 7.
Basically a wrapper around 'centos-package-cron' (https://github.com/wied03/centos-package-cron)

Switches:
-h: Show this help then exit
-d: Dry run. Only show information and exit. Do not prompt to install anything.
-y: Assume yes. Do not prompt before installing security updates.

Exit codes:
1: Error. Need to be root
2: Error. Missing package 'centos-package-cron'
3: Error. Incorrect switch
50: Ok. No security updates available.
100: Ok. Security updates available.
0: Ok. (Clean exit)

Author of centos-yum-security: 
Magnus Wallin <magnus.wallin@tutanota.com>

License of centos-yum-security:
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.
This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.
You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

Author of centos-package-cron:
Brady Wied <https://github.com/wied03>
License for centos-package-cron:
Copyright (c) 2016, BSW Technology Consulting LLC All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that
the following conditions are met:

· Redistributions of source code must retain the above copyright notice, this list of conditions and the 
following disclaimer.

· Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the 
following disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED 
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A 
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY 
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, 
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER 
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR 
OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF 
SUCH DAMAGE.
```

## Examples
### Running, and installing updates:
```
sudo centos-yum-security
Gathering information about packages needed for security. This will take a while...
8 packages needed for security:
dhclient-4.2.5-58.el7.centos.1
dhcp-common-4.2.5-58.el7.centos.1
dhcp-libs-4.2.5-58.el7.centos.1
kernel-3.10.0-514.el7
kernel-3.10.0-693.17.1.el7
kernel-tools-3.10.0-693.17.1.el7
kernel-tools-libs-3.10.0-693.17.1.el7
python-perf-3.10.0-693.17.1.el7
Install updates? [Y/N] y
Installing security updates...
Updating dhclient-4.2.5-58.el7.centos.1
Updating dhcp-common-4.2.5-58.el7.centos.1
Updating dhcp-libs-4.2.5-58.el7.centos.1
Updating kernel-3.10.0-514.el7
Updating kernel-3.10.0-693.17.1.el7
Updating kernel-tools-3.10.0-693.17.1.el7
Updating kernel-tools-libs-3.10.0-693.17.1.el7
Updating python-perf-3.10.0-693.17.1.el7
```

### Querying:
```
sudo centos-yum-security -d
Gathering information about packages needed for security. This will take a while...
73 packages needed for security:
authconfig-6.2.8-14.el7
bash-4.2.46-20.el7_2
bind-libs-lite-9.9.4-37.el7
bind-license-9.9.4-37.el7
[. . .]
vim-minimal-7.4.160-1.el7
wpa_supplicant-2.0-20.el7
```

## Installation:
Apart from this script, you need to install `centos-package-cron` and its
dependencies.

```
yum install mailx yum-plugin-changelog wget
```

Then check here for the latest `rpm`:
https://github.com/wied03/centos-package-cron/releases

Download the latest stable `rpm` using `wget`:
```
wget https://github.com/wied03/centos-package-cron/releases/download/releases/1.0.10/centos-package-cron-1.0-10.el7.centos.x86_64.rpm
```

Now install `centos-package-cron` and solve its dependencies:
```
sudo yum install centos-package-cron-1.0-10.el7.centos.x86_64.rpm
```
