Rust_Enclave_Name := libenclave.a
Rust_Enclave_Files := $(wildcard src/*.rs)
Rust_Target_Path := $(CURDIR)/../../../xargo
#Rust_Enclave_Profile := debug
Rust_Enclave_Profile := release
# Following doesn't seem to work - FIXME: This AND line 20 which has --release in it and SHOULD NOT!
#ifeq ($Rust_Enclave_Profile,release)
#    Cargo_Flags := --release
#endif

.PHONY: all

all: $(Rust_Enclave_Name)

$(Rust_Enclave_Name): $(Rust_Enclave_Files)
ifeq ($(XARGO_SGX), 1)
	RUST_TARGET_PATH=$(Rust_Target_Path) xargo build --target x86_64-unknown-linux-sgx $(Cargo_Flags)
	cp ./target/x86_64-unknown-linux-sgx/$(Rust_Enclave_Profile)/libethkey_sgx_enclave.a ../lib/libenclave.a
else
	cargo build -v --release $(Cargo_Flags)
	cp ./target/$(Rust_Enclave_Profile)/libethkey_sgx_enclave.a ../lib/libenclave.a
endif
