LIB_HOME = $(shell pwd)/source

all:	keys_test config_test
	$(MAKE) -C source PROGRAMS="dropbear"
	$(MAKE) -C source PROGRAMS="dropbear" install

keys_test:
	( if [ -f ./keys_done ]; then \
		echo "the same keys"; \
	else \
		echo "Generating keys"; \
		dropbearkey -t rsa -f $(LIB_HOME)/../dropbear_rsa_host_key ; \
		rm -f keys_done; \
		touch keys_done; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure; \
		rm -f config_done; \
		touch config_done; \
	fi ) 

configure:
	( cd source ; \
	./configure \
		--host=mipsel-linux \
		--prefix=$(LIB_HOME)/../install \
	)

clean:
	$(MAKE) -C source distclean
	rm -rf install
	rm -f config_done
	rm -f keys_done

romfs:
#	echo "do nothing"
	cp install/sbin/dropbear .
	$(STRIP) dropbear
	$(ROMFSINST) /sbin/dropbear
	$(ROMFSINST) -d /etc/dropbear/dropbear_rsa_host_key

