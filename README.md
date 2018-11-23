# WAS System Check Data Collection

## WAS Cell Configuration backup file

Note, this command only need to run on DMGR profile.

cd <WAS_INSTALL>/profiles/<DMGR_PROFILE>/bin

./backupConfig.sh <APP>_DMGR_Config_<dDATE>.zip -nostop


For example, in the DMGR machine,

cd /opt/ibm/websphere/AppServer/profiles/Dmgr01/bin
./backupConfig.sh TM_DMGR_Config_2018-11-20.zip -nostop

Note, the output file will be in the location where the command is run, e.g. /opt/ibm/websphere/AppServer/profiles/Dmgr01/bin

## WAS Cell Configuration Properties

Note, this command only need to run on DMGR profile.

Use the command below to extract the configuration for an entire cell.
./wsadmin.sh <wasuser> -password <password> -lang jython
wsadmin> AdminTask.extractConfigProperties('[-propertiesFileName <APP>.cell.props ]')


for example,

cd /opt/ibm/websphere/AppServer/profiles/Dmgr01/bin

./wsadmin.sh -user wasadmin -password password -lang jython

wsadmin> AdminTask.extractConfigProperties('[-propertiesFileName TM.cell.props ]')

Note, the output file will be in the location where the command is run, e.g. /opt/ibm/websphere/AppServer/profiles/Dmgr01/bin


## WAS Log Files

Note, please ensure "Verbose Garbage Collection" checkbox in WAS admoin console is checked.  Its navigation path is Application servers > [Target Server] > Process definition > Java Virtual Machine

For a cluster that has many application servers, you only need to enable verbose GC on 1 server.

We want the GC log has 48 hours data, to appropriately present runtime situation.

We want to collect the entire WAS cell log files. Collect all "logs" folders from all profiles of all WAS machines.

All server logs, including ffdc, SystemOut.log, SsytemErr.log, GC log (native_stderr.log), etc. Basically all log files are in the “logs” folder of all profiles on all WAS machines.

If possible, please archive existing logs folder and clean the logs directly, to make logs directory size smaller. 

One common issue in collecting logs is the logs directly filled with many GB history data from the past few years.  Good practice is to periodically archive and rotate log files to ensure the logs directory size is manageable.

