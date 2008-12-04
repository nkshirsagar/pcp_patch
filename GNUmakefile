#!gmake
#
# Copyright (c) 1997-2002 Silicon Graphics, Inc.  All Rights Reserved.
#
# $Id: GNUmakefile,v 1.10 2005/07/10 23:46:11 kenmcd Exp $
#

-include ./GNUlocaldefs

SUBDIRS = home

SHELL	= /bin/sh

PATH	= $(shell PATH=/sbin:/bin:/usr/sbin:/usr/bin . /etc/pcp.env; echo $$PATH)
MAKEOPTS = --no-print-directory

TESTS	= $(shell sed -e 's/ .*//' owner)

OTHERS	=

default:	new remake check qa_hosts $(OTHERS)

install:

default_pcp default_pro:

install_pcp install_pro:

src-pcp:

exports install:

clobber cleanup:
	rm -rf 051.work
	rm -f *.bak *.bad *.core *.full *.raw *.o core a.out core.*
	rm -f *.log eek* urk* so_locations tmp.* gmon.out oss.qa.tar.gz
	rm -f *.full.ok *.new rc_cron_check.clean
	rm -f sudo make.out qa_hosts localconfig localconfig.h check.time
	if [ -d src ]; then cd src; $(MAKE) clobber; else exit 0; fi
	if [ -d src-oss ]; then cd src-oss; $(MAKE) clobber; else exit 0; fi
	find ???.out ????.out -type f -links +1 | xargs rm -f
	rm -f 134.full.*
	# these ones are links to the real files created when the associated
	# test is run
	#
	rm -f 008.out 012.out 015.out 019.out 022.out 023.out 024.out 031.out \
	    033.out 044.out 051.out 062.out 066.out 067.out 069.out 075.out \
	    082.out 083.out 110.out 119.out 130.out 149.out 154.out \
	    158.out 159.out 160.out 162.out 180.out 183.out 188.out 190.out \
	    200.out 215.out 219.out 243.out 244.out 245.out 250.out 255.out \
	    262.out 278.out 282.out 299.out 313.out 355.out 365.out 375.out \
	    376.out 411.out 417.out 419.out 421.out 430.out 465.out 519.out \
	    555.out 558.out 560.out 565.out 569.out 574.out \
	    580.out 587.out 600.out 603.out 605.out

# 051 depends on this rule being here
051.work/die.001: 051.setup
	chmod u+x 051.setup
	./051.setup

sudo:	sudo.c
	cc -o sudo sudo.c
	chown root sudo
	chmod 4755 sudo
	@echo "NOTE sudo is a giant security hole, but this is needed by the PCP QA"

qa_hosts:	qa_hosts.master mk.qa_hosts
	PATH=$(PATH); ./mk.qa_hosts

setup:

PLATFORM=0
ifeq ($(PCP_PLATFORM), irix)
PLATFORM=1
endif
ifeq ($(PCP_PLATFORM), linux)
PLATFORM=2
endif

localconfig:
	PATH=$(PATH); ./mk.localconfig
