# WAS System Check Data Collection

## WAS Cell Configuration backup file

cd <WAS_INSTALL>/profiles/<DMGR_PROFILE>/bin

./backupConfig.sh <APP>_DMGR_Config_<dDATE>.zip -nostop


For example, in the DMGR machine,

cd /opt/ibm/websphere/AppServer/profiles/Dmgr01/bin
./backupConfig.sh TM_DMGR_Config_2018-11-20.zip -nostop

Note, the output file will be in the location where the command is run, e.g. /opt/ibm/websphere/AppServer/profiles/Dmgr01/bin

## WAS Cell Configuration Properties

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

We want to collect the entire WAS cell log files. Collect all "logs" folders from all profiles of all WAS machines.

All server logs, including ffdc, SystemOut.log, SsytemErr.log, GC log (native_stderr.log), etc. Basically all log files are in the “logs” folder of all profiles on all WAS machines.

