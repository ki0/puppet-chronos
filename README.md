# Puppet module: chronos

This is a Puppet module for chronos based on the second generation layout ("NextGen") of Example42 Puppet Modules.

Made by Enver Romon / Kimia Solutions S.L.

Official site: http://www.kimia.mobi

Official git repository: http://github.com/enverromon/puppet-chronos

Released under the terms of Apache 2 License.

This module requires functions provided by the Example42 Puppi module (you need it even if you don't use and install Puppi)

For detailed info about the logic and usage patterns of Example42 modules check the DOCS directory on Example42 main modules set.


## USAGE - Basic management

* Install chronos with default settings

        class { 'chronos': }

* Install a specific version of chronos package

        class { 'chronos':
          version => '1.0.1',
        }

* Disable chronos service.

        class { 'chronos':
          disable => true
        }

* Remove chronos package

        class { 'chronos':
          absent => true
        }

* Enable auditing without without making changes on existing chronos configuration *files*

        class { 'chronos':
          audit_only => true
        }

* Module dry-run: Do not make any change on *all* the resources provided by the module

        class { 'chronos':
          noops => true
        }


## USAGE - Overrides and Customizations
* Use custom sources for main config file

        class { 'chronos':
          source => [ "puppet:///modules/example42/chronos/chronos.conf-${hostname}" , "puppet:///modules/example42/chronos/chronos.conf" ],
        }


* Use custom source directory for the whole configuration dir

        class { 'chronos':
          source_dir       => 'puppet:///modules/example42/chronos/conf/',
          source_dir_purge => false, # Set to true to purge any existing file not present in $source_dir
        }

* Use custom template for main config file. Note that template and source arguments are alternative.

        class { 'chronos':
          template => 'example42/chronos/chronos.conf.erb',
        }

* Automatically include a custom subclass

        class { 'chronos':
          my_class => 'example42::my_chronos',
        }


## USAGE - Example42 extensions management
* Activate puppi (recommended, but disabled by default)

        class { 'chronos':
          puppi    => true,
        }

* Activate puppi and use a custom puppi_helper template (to be provided separately with a puppi::helper define ) to customize the output of puppi commands

        class { 'chronos':
          puppi        => true,
          puppi_helper => 'myhelper',
        }

* Activate automatic monitoring (recommended, but disabled by default). This option requires the usage of Example42 monitor and relevant monitor tools modules

        class { 'chronos':
          monitor      => true,
          monitor_tool => [ 'nagios' , 'monit' , 'munin' ],
        }

* Activate automatic firewalling. This option requires the usage of Example42 firewall and relevant firewall tools modules

        class { 'chronos':
          firewall      => true,
          firewall_tool => 'iptables',
          firewall_src  => '10.42.0.0/24',
          firewall_dst  => $ipaddress_eth0,
        }


## CONTINUOUS TESTING

Travis {<img src="https://travis-ci.org/example42/puppet-chronos.png?branch=master" alt="Build Status" />}[https://travis-ci.org/example42/puppet-chronos]
