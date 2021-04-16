include ../../../Makefile.versions

TESTS += test_sub
TESTS += test_self
TESTS += test_notify
TESTS += test_iters
TESTS += test_errno

all: $(TESTS)
.PHONY: all

run: all
	./run.sh
.PHONY: run

define genb
$(1): $(1).o lib.o
	gcc $$^ -L ../../../lib/c/ -L ../../../images/ -lcriu -o $$@
endef

$(foreach t, $(TESTS), $(eval $(call genb, $(t))))

%.o: %.c
	gcc -c $^ -iquote ../../../criu/include -I../../../lib/c/ -I../../../images/ -o $@ -Werror

clean: libcriu_clean
	rm -rf $(TESTS) $(TESTS:%=%.o) lib.o
.PHONY: clean

libcriu_clean:
	rm -f libcriu.so.${CRIU_SO_VERSION_MAJOR}
.PHONY: libcriu_clean

libcriu:
	ln -s ../../../lib/c/libcriu.so libcriu.so.${CRIU_SO_VERSION_MAJOR}
.PHONY: libcriu
