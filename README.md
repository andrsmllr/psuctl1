# PSU CONTROL UTILITY KIPRIM DC310S

`psuctl1` is a simple shell script to control a PSU from a Linux/Unix terminal.  
Compatible PSUs are variants of the `Owon`, for example the `KIPRIM DC310S`.  

## Usage

~~~shell
psuctl1 help
Usage: psuctl1 [-t tty] [-v] current|help|id|output|power|voltage get|measure|set [value]

    value: a decimal value with up to 2 digits and up to 3 decimals (dd.ddd)
           value is only required when using the 'set' command and is otherwise ignored
           for the 'output' command, value must be 0 (off) or 1 (on)

    Options:
        -t tty   specify the tty device (default: /dev/ttyUSB0)
        -v       verbose output

    Examples: 1) psuctl1 voltage get
              2) psuctl1 v g
              3) psuctl1 voltage set 3.300
              4) psuctl1 v s 3.3

    Commands:
        current      get|measure|set [value]  -  get, measure or set the output current
        currentlimit get|set         [value]  -  get or set the current limit
        output       get|set         [0|1]    -  get or set the output state (0=off, 1=on)
        power        measure                  -  measure the output power
        voltage      get|measure|set [value]  -  get, measure or set the output voltage
        voltagelimit get|set         [value]  -  get or set the voltage limit

    Commands can be shortened in various ways, e.g. 'v' for 'voltage' and 'g' for 'get'.

    The following abbreviations are recognized:
        current, curr, c
        currentlimit, currlimit, currl, climit, clim, cl
        measure, meas, m
        output, out, o
        power, pow, p
        voltage, volt, v
        voltagelimit, voltlimit, voltl, vlimit, vlim, vl

    If the second argument (i.e. get|measure|set) is ommitted then 'get' will be assumed.
    In case the 'get' sub-command does not exist, then 'measure' is assumed.

# Short-hand command
psuctl1 h
~~~

The `set` and `get` commands control the *nominal* value for voltage and current which the PSU shall provide.  
The `measure` command return the *actual* value for voltage and current that the PSU outputs.  

### Turn PSU Outputs ON and OFF

~~~shell
# Turn PSU voltage/current output on
psuctl1 output set 1
# Short-hand
psuctl1 o s 1

# Turn PSU voltage/current output off
psuctl1 output set 0
# Short-hand
psuctl1 o s 0
~~~

### Read Output Voltage

~~~shell
psuctl1 voltage get

# Short-hand command
psuctl1 v g
~~~

### Read Output Current

~~~shell
psuctl1 current get

# Short-hand command
psuctl1 c g
~~~

### Set Output Voltage

~~~shell
psuctl1 voltage set 3.3

# Short-hand command
psuctl1 v s 3.3
~~~

### Set Output Current

~~~shell
psuctl1 current set 1.0

# Short-hand command
psuctl1 c s 1.0
~~~

### Measure Output Voltage

~~~shell
psuctl1 voltage measure

# Short-hand command
psuctl1 v m
~~~

### Measure Output Current

~~~shell
psuctl1 current measure

# Short-hand command
psuctl1 c m
~~~

### Read PSU Identification

~~~shell
psuctl1 id
~~~

### Print Version of psuctl1

~~~shell
psuctl1 version
~~~

## Dependencies

`stty` is used to set the parameter of the serial interface (optional).  
`lsusb` and `readlink` are used to try to automatically find a USB-serial-device with a compatible PSU attached (optional).  
`getopts` (bashism) is used to parse command line options (optional).

## References

* [maximweb/kiprim-dc310s](https://github.com/maximweb/kiprim-dc310s) (+1 gratitude for documentation)
* [KIPRIM DC310S PSU](https://kiprim.de/?shpxid=1d4572e4-9ff8-4b03-9db7-ad52334c43a7)
* [OWON SPE3101 Manual](https://files.owon.com.cn/probook/SPS_Series_Power_Supply_User_Manual.pdf)
* [OWON Serial Commands Manual](https://files.owon.com.cn/software/Application/SP_and_SPE_SPS_programming_manual.pdff)
