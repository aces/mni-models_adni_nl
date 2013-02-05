AUTOMAKE_OPTIONS = check-news
ACLOCAL_AMFLAGS = -I local_m4

MNI_MODELS := mni-models

# mess with the data install directory
pkgdatadir = $(prefix)/share/$(MNI_MODELS)

MODEL_BASE := mni_adni
PRIM_MODAL := t1w_tal_nlin_asym
MODELS := $(MODEL_BASE)_$(PRIM_MODAL)

# datestamp
DATE_STAMP := `date +%D-%T`

# package data
dist_pkgdata_DATA := \
	$(MODELS:=.mnc.gz) \
	$(MODEL_BASE)_$(PRIM_MODAL)_mask.mnc.gz \
	$(MODEL_BASE)_$(PRIM_MODAL)_mask.obj.gz \
	$(MODEL_BASE)_$(PRIM_MODAL)_headmask.mnc.gz \
        $(MODEL_BASE)_$(PRIM_MODAL)_vent.mnc.gz \
        $(MODEL_BASE)_$(PRIM_MODAL)_vent.obj.gz

## mni_adni_t1w_tal_nlin_asym_ntags_1000_bg.tag
## mni_adni_t1w_tal_nlin_asym_ntags_1000_nobg.tag
## 
## Cerebellum_Ventricles_SubCortical_Mask-ADNI.mnc


# installed data data
pkgdata_DATA := \
	$(MODELS:=.mnc) \
	$(MODELS:=_mask.mnc) \
	$(MODELS:=_mask.obj) \
	$(MODELS:=_headmask.mnc) \
	$(MODELS:=_vent.mnc) \
	$(MODELS:=_vent.obj) \
	$(MODELS:=_16_blur.mnc) \
	$(MODELS:=_16_mask.mnc) \
	$(MODELS:=_2_blur.mnc) \
	$(MODELS:=_2_dxyz.mnc) \
	$(MODELS:=_2_mask.mnc) \
	$(MODELS:=_4_blur.mnc) \
	$(MODELS:=_4_dxyz.mnc) \
	$(MODELS:=_4_mask.mnc) \
	$(MODELS:=_8_blur.mnc) \
	$(MODELS:=_8_dxyz.mnc) \
	$(MODELS:=_8_mask.mnc)

EXTRA_DIST = $(m4_files) \
	epm-header.in \
        mni_adni_t1w_tal_nlin_asym_ntags_1000_bg.tag \
        mni_adni_t1w_tal_nlin_asym_ntags_1000_nobg.tag \
        Cerebellum_Ventricles_SubCortical_Mask-ADNI.mnc

m4_files = local_m4/ac_prog_gzip.m4 \
	local_m4/ac_prog_make_model.m4

# be tidy
CLEANFILES = $(pkgdata_DATA) $(MODELS:=.mnc)

# gunzip rule
%: %.gz
	$(gzip) -d -c $< > $@

all: $(dist_pkgdata_DATA:.gz=) $(DATE)
	for i in $(MODELS); \
	do \
		echo "Doing $$i"; \
		for m in mask headmask; \
		do \
			echo "Checking for $$i\_$$m.mnc"; \
			if [ ! -e $$i\_$$m.mnc ]; \
			then \
				ln -s $(MODEL_BASE)_$(PRIM_MODAL)_$$m.mnc $$i\_$$m.mnc; \
			fi \
		done; \
      $(make_model) $$i; \
	done
	for i in $(pkgdata_DATA); \
   do \
      echo "Adding mni-model header to $$i"; \
      minc_modify_header \
			-sinsert mni-model:package=$(PACKAGE) \
			-sinsert mni-model:version=$(VERSION) \
			-sinsert mni-model:compile-date=$(DATE_STAMP) \
			-sinsert mni-model:compile-user=$$USER \
			$$i; \
   done
