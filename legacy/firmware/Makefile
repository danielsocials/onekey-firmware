APPVER = 1.8.0

NAME = onekey

ifeq ($(EMULATOR),1)
OBJS += udp.o
else
ifeq ($(ONEKEY_MINI),1)
OBJS += font_ex.o
OBJS += device2.o
OBJS += flash_enc.o
OBJS += nft.o
endif
OBJS += usb.o
OBJS += bl_check.o
OBJS += header.o
endif

OBJS += font.o
OBJS += chinese.o
OBJS += gettext.o
OBJS += language.o
OBJS += menu_para.o
OBJS += menu_core.o
OBJS += menu_list.o
OBJS += messages.o
OBJS += config.o
OBJS += trezor.o
OBJS += pinmatrix.o
OBJS += fsm.o
OBJS += coins.o
OBJS += coin_info.o
OBJS += transaction.o
OBJS += protect.o
OBJS += layout2.o
OBJS += recovery.o
OBJS += reset.o
OBJS += signing.o
OBJS += crypto.o

ifneq ($(BITCOIN_ONLY),1)
OBJS += u2f.o
OBJS += ethereum.o
OBJS += ethereum_tokens.o
OBJS += lisk.o
OBJS += nem2.o
OBJS += nem_mosaics.o
OBJS += stellar.o
OBJS += solana.o
endif

OBJS += debug.o

OBJS += ../vendor/trezor-crypto/address.o
OBJS += ../vendor/trezor-crypto/bignum.o
OBJS += ../vendor/trezor-crypto/ecdsa.o
OBJS += ../vendor/trezor-crypto/curves.o
OBJS += ../vendor/trezor-crypto/secp256k1.o
OBJS += ../vendor/trezor-crypto/nist256p1.o
OBJS += ../vendor/trezor-crypto/hmac_drbg.o
OBJS += ../vendor/trezor-crypto/rfc6979.o
OBJS += ../vendor/trezor-crypto/rand.o
OBJS += ../vendor/trezor-crypto/memzero.o

OBJS += ../vendor/trezor-crypto/ed25519-donna/curve25519-donna-32bit.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/curve25519-donna-helpers.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/modm-donna-32bit.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/ed25519-donna-basepoint-table.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/ed25519-donna-32bit-tables.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/ed25519-donna-impl-base.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/ed25519.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/curve25519-donna-scalarmult-base.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/ed25519-sha3.o
OBJS += ../vendor/trezor-crypto/ed25519-donna/ed25519-keccak.o

OBJS += ../vendor/trezor-crypto/hmac.o
OBJS += ../vendor/trezor-crypto/bip32.o
OBJS += ../vendor/trezor-crypto/bip39.o
OBJS += ../vendor/trezor-crypto/pbkdf2.o
OBJS += ../vendor/trezor-crypto/base32.o
OBJS += ../vendor/trezor-crypto/base58.o
OBJS += ../vendor/trezor-crypto/segwit_addr.o
OBJS += ../vendor/trezor-crypto/cash_addr.o

OBJS += ../vendor/trezor-crypto/ripemd160.o
OBJS += ../vendor/trezor-crypto/sha2.o
OBJS += ../vendor/trezor-crypto/sha3.o
OBJS += ../vendor/trezor-crypto/blake256.o
OBJS += ../vendor/trezor-crypto/blake2b.o
OBJS += ../vendor/trezor-crypto/groestl.o
OBJS += ../vendor/trezor-crypto/hasher.o

OBJS += ../vendor/trezor-crypto/aes/aescrypt.o
OBJS += ../vendor/trezor-crypto/aes/aeskey.o
OBJS += ../vendor/trezor-crypto/aes/aestab.o
OBJS += ../vendor/trezor-crypto/aes/aes_modes.o

OBJS += ../vendor/trezor-crypto/chacha20poly1305/chacha20poly1305.o
OBJS += ../vendor/trezor-crypto/chacha20poly1305/chacha_merged.o
OBJS += ../vendor/trezor-crypto/chacha20poly1305/poly1305-donna.o
OBJS += ../vendor/trezor-crypto/chacha20poly1305/rfc7539.o

OBJS += ../vendor/trezor-crypto/nem.o

OBJS += ../vendor/QR-Code-generator/c/qrcodegen.o

OBJS += ../vendor/trezor-storage/storage.o
OBJS += ../vendor/trezor-storage/norcow.o

OBJS += ../vendor/nanopb/pb_common.o
OBJS += ../vendor/nanopb/pb_decode.o
OBJS += ../vendor/nanopb/pb_encode.o

OBJS += protob/messages.pb.o
OBJS += protob/messages-bitcoin.pb.o
OBJS += protob/messages-common.pb.o
OBJS += protob/messages-crypto.pb.o
OBJS += protob/messages-debug.pb.o
OBJS += protob/messages-management.pb.o
ifneq ($(BITCOIN_ONLY),1)
OBJS += protob/messages-ethereum.pb.o
OBJS += protob/messages-lisk.pb.o
OBJS += protob/messages-nem.pb.o
OBJS += protob/messages-stellar.pb.o
OBJS += protob/messages-solana.pb.o
endif

OPTFLAGS ?= -Os

../vendor/trezor-crypto/bip32.o: OPTFLAGS = -O3
../vendor/trezor-crypto/bip39.o: OPTFLAGS = -O3
../vendor/trezor-crypto/ecdsa.o: OPTFLAGS = -O3
../vendor/trezor-crypto/sha2.o: OPTFLAGS = -O3
../vendor/trezor-crypto/secp256k1.o: OPTFLAGS = -O3

include ../Makefile.include

DEBUG_LINK ?= 0
DEBUG_LOG  ?= 0

ifeq ($(EMULATOR),1)
CFLAGS += --warn-no-unused-parameter
endif
CFLAGS += -fstack-protector-all
CFLAGS += -Wno-sequence-point
CFLAGS += -I../vendor/nanopb -Iprotob -DPB_FIELD_16BIT=1 -DPB_ENCODE_ARRAYS_UNPACKED=1 -DPB_VALIDATE_UTF8=1
CFLAGS += -DDEBUG_LINK=$(DEBUG_LINK)
CFLAGS += -DDEBUG_LOG=$(DEBUG_LOG)
CFLAGS += -DSCM_REVISION='"$(shell git rev-parse HEAD | sed 's:\(..\):\\x\1:g')"'
CFLAGS += -DUSE_MONERO=0
ifneq ($(BITCOIN_ONLY),1)
CFLAGS += -DUSE_ETHEREUM=1
CFLAGS += -DUSE_NEM=1
MAKO_RENDER_FLAG =
else
CFLAGS += -DUSE_ETHEREUM=0
CFLAGS += -DUSE_NEM=0
MAKO_RENDER_FLAG = --bitcoin-only
endif

%:: %.mako defs
	@printf "  MAKO    $@\n"
	$(Q)$(PYTHON) ../vendor/trezor-common/tools/cointool.py render $(MAKO_RENDER_FLAG) $@.mako

bl_data.h: bl_data.py bootloader.dat
	@printf "  PYTHON  bl_data.py\n"
	$(Q)$(PYTHON) bl_data.py

clean::
	rm -f bl_data.h
	find -maxdepth 1 -name "*.mako" | sed 's/.mako$$//' | xargs rm -f
