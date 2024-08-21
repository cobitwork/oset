# Makefile
#
# Copyright (C) 2000 Ivan Tubert and Eduardo Tubert
# 
# Contact: tubert@eros.pquim.unam.mx
# 
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
# All we ask is that proper credit is given for our work, which includes
# - but is not limited to - adding the above copyright notice to the beginning
# of your source code files, and to any copyright notice that you may distribute
# with programs based on this work.
# 
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA  02111-1307, USA. 
# 

CGIBIN_DIR = cgi-bin

.PHONY: all clean

OSETOBJS = mollib/_chem.o mollib/_clas2.o mollib/_error.o mollib/_execute.o mollib/_expr.o mollib/_fgfind.o mollib/_funcgrp.o mollib/_generat.o mollib/_moltopo.o mollib/_molgeom.o mollib/_molmem.o mollib/_molfile.o mollib/_parser.o mollib/_scanner.o mollib/_sym.o mollib/_analyze.o mollib/_log.o mollib/_path.o mollib/_complex.o mollib/_smiles.o mollib/_canon.o mollib/_logf2.o mollib/_smdb.o mollib/_molring.o mollib/_bitset.o mollib/_aroma.o mollib/_bigsmdb.o mollib/_sk2.o mollib/_sk2aux.o mollib/_sk2style.o mollib/_sk2obj.o mollib/_mol2sk2.o
SERVEROBJS = server/_thrlow.o server/_writesk.o server/_moltran.o server/_socklow.o server/server.o 
CPPFLAGS = -D_DEBUG -DLINUX

all: server oset cgi
server: $(OSETOBJS) $(SERVEROBJS)
	cc -o server/server $(OSETOBJS) $(SERVEROBJS) -m -lpthread

oset: $(OSETOBJS) oset/oset.o
	cc -o oset/oset -lm -lpthread $(OSETOBJS) oset/oset.o -lm -lpthread

cgi: cgi/startan.o cgi/savemol.o cgi/loadmol.o cgi/loadmol_marvin.o 
	@if [ ! -d $(CGIBIN_DIR) ]; then \
		echo ";; mkdir $(CGIBIN_DIR)"; mkdir $(CGIBIN_DIR); \
	fi
	cc -o cgi-bin/startan cgi/startan.o
	cc -o cgi-bin/loadmol cgi/loadmol.o
	cc -o cgi-bin/savemol.mol cgi/savemol.o
	cc -o cgi-bin/loadmol_marvin cgi/loadmol_marvin.o
clean:
	-rm -f mollib/*.o
	-rm -f server/server server/*.o
	-rm -f oset/oset oset/oset.o
	-rm -rf cgi-bin
