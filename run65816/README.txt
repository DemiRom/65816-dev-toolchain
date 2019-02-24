Ed Spittles
2009-03-28

run65816.c is a minimal BBC-micro emulator based on a test program
posted on 6502.org by Samuel A. Falvo II aka kc5tja and also based
on run6502 by Ian Piumarta which forms part of his lib6502 package

it emulates a BBC micro with a 65816, additional RAM, and some
supporting decode logic.

usage:
  ./run65816 -B -l c000 ../rom-images/OS12.ROM \
     ../rom-images/BASIC2.ROM ../boot816/boot816.bin

the Makefile is adjusted to build run65816 as well as lib65816

lib65816 has been tweaked to support run65816:
  src/dispatch.c
     to use the new M_FETCH instead of M_READ for instruction fetches
     to resurrect the E_UPDATE cycle count mechanism for regular IRQs
  config.mk 
     to pick up CCOPTS and to add the -g flag to cc
     to default CCOPTS to add -DDEBUG -DOLDCYCLES for tracing and E_UPDATE
  lib65816/cpu.h
     to define the new M_FETCH

TODO/BUGS
  BRK is handled by appropriating the WDM opcode hook
  WDM is not available to trigger tracing or stack dumps
  IRQ vector is pulled from bank0, with no easy way to emulate hardware redirection
  Most of the run6502 command line interface is not ported
  There's no means of selecting non-BBC or other hardware variants
  There's no command line interface to the tracing capability
  The regular IRQs are done using a deprecated mechanism
  The regular IRQs are not done by emulating VIA hardware
  Should handle Vector Pull and Valid Program Address by passing up from lib65816 to the emulator

Licensed as GPL v2
Copyright 2009-2010 Ed.Spittles@gmail.com

This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License
as published by the Free Software Foundation; either version 2
of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.
 
You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.

http://www.gnu.org/licenses/gpl-2.0.html
