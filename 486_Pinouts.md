# 486 Processors Pinout Differences

This document is organized bottom to top, with the relevant for the motherboard implementation information on the top and raw data on the bottom

## Signal Groups (Socket 3 Pin Numbers)
* NMI and Floating point error (FERR#, IGNNE#, NMI)
  * Pin B14 - FERR# on Intel 487SX and Overdrive processors; Pin D15 - FERR# on all DX processors; No FERR# pin on Intel 486SX processors
    * **Use a 3-position jumper to switch #FERR between B14 (487SX/Overdrive), D15 (486DX/5x86), or no connecton (486SX)**
  * Pin B16 - NMI on Intel 486SX, IGNNE# - on all other processors ; Pin C16 - NMI on all processors except of Intel 486SX
    * **Use a 3-position jumper to switch pin B16 between NMI (486SX) and IGNNE# (486DX/5x86)**
    * **Use a 2-position jumper to connect pin C16 to NMI (486DX/5x86)** (check if C16 is INC on 486SX, in this case jumper is not required) 
* Upgrade/overdrive processor support (UP#/MP#)
  * Pin C15 - MP#(P23N)/UP#(P24T) - CPU output; CPU drives this pin low to indicate that an overdrive processor is present
    * **No connect**
  * Pin D12 - MP#(P23S)/UP# - CPU input; CPU powers down cores and three-states outputs when this pins low
    * **No connect - Internal pull-up in the CPU**
* JTAG (TCK, TDI, TMS, TDO)
  * Pins: B4 - TCK, B15 - TDI, C15 - TMS, C17 - TDO
  * Supported on some processors (Intel DX*, AMD, Intel-compatible DX4/5x86 IBM, SGS and Cyrix)
    * **No connect (if JTAG is not used) - Internal pull-ups in the CPU**
* Suspend (SUSP#/STPCLK#, SUSPA#)
  * Pin H16 - SUSP#/STPCLK# - Input, used to request the CPU to stop system clock
    * **No connect - Internal pull-up in the CPU**
  * Pin B11 - SUSPA# (IBM/SGS/Cyrix/TI only) - Output, stop clock acknowledge (Intel uses Stop Grant bus cycle instead)
    * Note - Pin B11 is INV/INVAL input on Intel/Intel compatible CPUs with write-back cache
* Write-back Cache Support
  * Pin B11 (T5 on some IBM/SGS/TI CPUs) - INV/INVAL - Input, active during EADS# cycle indicates invalid cache line
  * Pin C14 (Intel and AMD Write-back CPUs) - WB/WT# - Input (pull-up to enable write-back?)
  * Pin B13 (Intel, and Intel compatible) / S18 (some IBM/SGS/TI CPUs) / U1 (Intel P24T) - HITM# - Output, active during cache inquiry cycle, indicating durty data in the L1 cache
  * Pin U2 (Intel P24T only) - HIT#
  * Pin G1 (Intel P24T) - CACHE#
* Cache Status Monitoring - IBM/SGS/Cyrix/TI (RPLVAL#, RPLSET0, RPLSET1)
  * Pin D14 (Pin C14 for for Intel Compatible DX4/5x86) - RPLVAL#
  * Pin D13 (Pin C15 for Intel Compatible DX4/5x86) - RPLSET0
  * Pin B14 (Pin C13 for Intel Compatible DX4/5x86) - RPLSET1
    * **Outputs - no connect**
* SMI (SRESET/WM_RST, SMI#, SMIACT#/SMADS#)
  * SRESET/WM_RST
  * Pin (B13 on some IBM/SGS/TI CPUs) - SMI#
  * SMIACT#/SMADS#
    * **No connect - Internal pull-ups in the CPU?**
* Low voltage support
  * VOLDET - Low (0) for low voltage (3.3V, 3.45V), High (1) For 5V
  * Vcc5 - Reference I/O voltage (Intel 486DX4) - 5V for 5V I/O. Should be tied up with 100 ohm resistor?

## Pinout Differences

* Pin A3 (Socket 1) / Pin B4 (Socket 3)
  * TCK: Intel: ODPR-S, P4, P4S, P24, P24S, P24C, P24D; AMD: 486DX2, 486DX2W, 486DX4, 486DX4W; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin A10 (Socket 1) / Pin B11 (Socket 3)
  * SUSPA#: IBM: 486DX, 486DXV, 486DX2, 486DX2V, 486DX4; SGS: 486DX, 486DX2
  * INV/INVAL (IBM, SGS, Cyrix): Intel: P24D; IBM: 486DX4W, 5x86C; AMD: 486DX2, 486DX2W, 486DX4, 486DX4W, 5x86; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin A12 (Socket 1) / Pin B13 (Socket 3)
  * HITM#: Intel: P24D; IBM 486DX4W, 5x86C; AMD: 486DX2W, 486DX4W, 5x86; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * SMI#: IBM:	486DX, 486DXV, 486DX2, 486DX2V, 486DX4
  * NC/INC: Other CPUs
* Pin A13	(Socket 1) / Pin B14 (Socket 3)
  * FERR#: Intel: P23N, ODP, ODP-S, P24T
  * RPLSET1: IBM: 486DX, 486DXV, 486DX2, 486DX2V, 486DX4; SGS: 486DX, 486DX2
  * SUSPA#: IBM: 486DX4W, 5x86C; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin A14	(Socket 1) / Pin B15 (Socket 3)
  * TDI: Intel: ODPR-S, P4, P4S, P24, P24S, P24C, P24D; IBM: 486DX4W, 5x86C; AMD: 486DX2, 486DX2W, 486DX4, 486DX4W; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin A15	(Socket 1) / Pin B16 (Socket 3)
  * NMI: Intel P23, Intel P23S
  * IGNNE#: Other CPUs
* Pin B10	(Socket 1) / Pin C11 (Socket 3)
  * SMI#: Intel:	P23S, P23N, ODP-S, ODPR-S, P4S, P24S, P24C, P24D, P24T; IBM: 5x86C; AMD: 486DX2W, 486DX4W, 5x86; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin B12	(Socket 1) / Pin C13 (Socket 3)
  * CACHE#: Intel P24D, IBM 5x86C, AMD 486DX2W, AMD	486DX4W, AMD 5x86, SGS 5x86, Cyrix 5x86
  * TEST: IBM	486DX, IBM 486DXV, IBM 486DX2, IBM 486DX2V
  * RPLSET1: IBM 486DX4W, SGS 486DX2V
  * NC/INC: Other CPUs
* Pin B13	(Socket 1) / Pin C14 (Socket 3)
  * WB/WT#: Intel P24D, IBM 5x86C, AMD 486DX2W, AMD 486DX4W, AMD 5x86
  * WM_RST: IBM 486DX, IBM 486DXV, IBM 486DX2, IBM 486DX2V, IBM 486DX4, SGS 486DX, SGS 486DX2
  * RPLVAL#: IBM 486DX4W, SGS 486DX2V, SGS 5x86
  * CLKMUL: AMD 486DX2, AMD 486DX4
  * NC/INC: Other CPUs
* Pin B14	(Socket 1) / Pin C15 (Socket 3)
  * MP#/UP#: Intel: P23N, ODP, ODP-S, P24T
  * TMS: Intel: ODPR-S, P4, P4S, P24, P24S, P24C, P24D; IBM: 486DX4W, x86C; AMD: 486DX2, 486DX2W, 486DX4, 486DX4W; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * RPLSET0: IBM 486DX4W, SGS	486DX2V, SGS 5x86
* Pin B15	(Socket 1) / Pin C16 (Socket 3)
  * NC: Intel P23, P23S
  * NMI: Other CPUs
* Pin B16	(Socket 1) / Pin C17 (Socket 3)
  * TDO: Intel: ODPR-S, P4, P4S, P24, P24S, P24C, P24D; IBM: 486DX4W, x86C; AMD: 486DX2, 486DX2W, 486DX4, 486DX4W; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin C10	(Socket 1) / Pin D11 (Socket 3)
  * SRESET/WM_RST (IBM, SGS, Cyrix): Intel: P23S, P23N, ODP-S, ODPR-S, P4S,	P24S,	P24C, P24D; AMD: 486DX2W, 486DX4W, 5x86; IBM: 486DX4W, 5x86C; SGS:	486DX2V, 5x86, Cyrix: 5x86
  * SMADS#: IBM: 486DX, 486DXV, 486DX2, 486DX2V, 486DX4; SGS: 486DX, 486DX2
  * NC/INC: Other CPUs
* Pin C11	(Socket 1) / Pin D12 (Socket 3)
  * MP#/UP#: Intel: P23S, Intel ODPR-S, P4, P4S, P24, P24S, P24C, P24D; AMD: 486DX2, 486DX2W, 486DX4, 486DX4W, 5x86; SGS: 486DX, 486DX2, 486DX2V, 5x86; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin C12	(Socket 1) / Pin D13 (Socket 3)
  * SMIACT#/SMADS# (IBM, SGS, Cyrix): Intel: P23S, P23N, ODP-S, ODPR-S, P4S, P24S, P24C, P24D, P24T; AMD: 486DX2W, 486DX4W, AMD 5x86; IBM:	486DX4W, 5x86C; SGS 486DX, 486DX2, 486DX2V, 5x86; Cyrix 5x86
  * RPLSET0: IBM: 486DX, 486DXV, 486DX2, 486DX2V, 486DX4
  * NC/INC: Other CPUs
* Pin C13	(Socket 1) / Pin D14 (Socket 3)
  * RPLVAL#: IBM: 486DX, 486DXV, 486DX2, 486DX2V, 486DX4; SGS: 486DX, 486DX2
  * TEST: IBM: 486DX4W, 5x86C; SGS: 486DX2V, 5x86
  * NC: Other CPUs
* Pin C14	(Socket 1) / Pin D15 (Socket 3)
  * NC: Intel: ODP (check if it is INC)
  * INC: Intel: P23, P23S, P23N, P24T
  * FERR#: Other CPUs
* Pin D4	(Socket 1) / Pin E5 (Socket 3)
  * KEY (pin): Intel: P23N, ODP, ODP-S
  * No pin: Other CPUs
* Pin G15	(Socket 1) / Pin H16 (Socket 3)
  * STPCLK#/SUSP# (IBM, SGS, Cyrix): Intel: P23S, P23N, ODP-S, ODPR-S, P4S, P24S, P24C, P24D, P24T; AMD: 486DX2W, 486DX4W, 5x86; IBM: 486DX, 486DXV, 486DX2, 486DX2V, 486DX4, 486DX4W, 5x86C; SGS: 486DX, 486DX2, 486DX2V, 5x86; Cyrix: 5x86
  * NC/INC: Other CPUs
* Pin J1	(Socket 1) / Pin K2 (Socket 3)
  * Vcc5: Intel P24C
  * INC: AMD: 486DX2
  * NC: IBM: 486DXV, 486DX2V, 486DX4, 486DX4W, 5x86C; SGS: 486DX, 486DX2, 486DX2V, 5x86; Cyrix 5x86
  * Vcc: Other CPUs (how is it defined in 3.3V/3.45V CPUs?)
* Pin R17	(Socket 1) / Pin S18 (Socket 3)
  * CLKMUL: Intel: P24C, IBM 486DX4W, 5x86C; AMD: 486DX2W, 486DX4W, 5x86; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * HITM#: IBM: 486DX,	486DXV, 486DX2, 486DX2V, 486DX4; SGS: 486DX, 486DX2
  * NC/INC: Other CPUs
* Pin S5	(Socket 1) / Pin T6 (Socket 3)
  * VOLDET: Intel: P24C; IBM: 5x86C; AMD: 486DX2, 486DX2W, 486DX4, 486DX4W, 5x86; SGS: 486DX2V, 5x86; Cyrix: 5x86
  * BRDYC#: Intel: P23S, P4S, P24S
  * INVAL: IBM: 486DX, 486DXV, 486DX2, 486DX2V, 486DX4; SGS: 486DX, 486DX2
  * Vss: IBM: 486DX4W
  * NC: Other CPUs
* P24T (Socket 3) only pins:
  * F19 - SRESET
  * G1 - CACHE#
  * N1 - INV
  * T1 - WB/WT#
  * U1 - HITM#
  * U2 - HIT#

Are these the same pins
* INV ?= INVAL (IBM, SGS, Cyrix)
* SRESET == INIT (P24T) ?= WM_RST (IBM, SGS, Cyrix)
* SMIACT# ?= 
* STPCLK# ?= SUSP# (IBM, SGS, Cyrix)

## Sources

* [486 Pinouts](http://www.pchardwarelinks.com/486pin2.htm), Chris Hare, 2001
* [Intel Pentium* Overdrive* Processor](http://datasheets.chipdb.org/Intel/x86/486/applnots/29043606.PDF), Datasheet,  Order Number 290544-001, Intel Corp., June 1995
* [IBM Microelectronics 486DX2 Common Socket Specification For 168 PGA Socket](http://datasheets.chipdb.org/IBM/x86/486/40004.PDF) Application Note, Fax# 40004, IBM Corp., May 23rd, 1995
