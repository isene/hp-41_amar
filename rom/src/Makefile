RPN_SRCS = AMAR.rpn O6.rpn ENC.rpn ENCTYP.rpn ENCNUM.rpn ENCAT.rpn TERRE.rpn STATS.rpn ENCDAT.rpn
RPN_RAWS =
ASM_SRCS = header.s

OBJS = $(RPN_SRCS:%.rpn=%.o) $(RPN_RAWS:%.raw=%.o) $(ASM_SRCS:%.s=%.o)

MOD = AMAR.mod

all:	$(MOD)

clean:
	-rm -f ${OBJS} *.lst $(MOD)

%.o: %.rpn
	rpncomp -l $<

%.o: %.raw
	rpncomp -l $<

%.o: %.s
	asnut $<

$(MOD): $(OBJS) AMAR.scm AMAR.moddesc Makefile
	lnnut -l $(OBJS) AMAR.scm AMAR.moddesc --no-list-header -o $(MOD)
