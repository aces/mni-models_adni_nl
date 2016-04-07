AUTOMAKE_OPTIONS = check-news
ACLOCAL_AMFLAGS = -I local_m4

MNI_MODELS := mni-models

# mess with the data install directory
pkgdatadir = $(prefix)/share/$(MNI_MODELS)
tagdir = $(prefix)/share/classify-ADNI
pvedir = $(prefix)/share/pve

MODEL_BASE := mni_adni
ASYM_MODEL := t1w_tal_nlin_asym
SYM_MODEL := hi_t1w_tal_nlin_sym
MODELS := $(MODEL_BASE)_$(ASYM_MODEL) $(MODEL_BASE)_$(SYM_MODEL)

# datestamp
DATE_STAMP := `date +%D-%T`

# package data
dist_pkgdata_DATA := \
	$(MODELS:=.mnc.gz) \
	$(MODEL_BASE)_$(ASYM_MODEL)_mask.mnc.gz \
	$(MODEL_BASE)_$(ASYM_MODEL)_mask.obj.gz \
	$(MODEL_BASE)_$(ASYM_MODEL)_headmask.mnc.gz \
        $(MODEL_BASE)_$(ASYM_MODEL)_vent.mnc.gz \
        $(MODEL_BASE)_$(ASYM_MODEL)_vent.obj.gz \
	$(MODEL_BASE)_$(SYM_MODEL)_mask.mnc.gz \
	$(MODEL_BASE)_$(SYM_MODEL)_mask.obj.gz \
	$(MODEL_BASE)_$(SYM_MODEL)_headmask.mnc.gz \
        $(MODEL_BASE)_$(SYM_MODEL)_vent.mnc.gz \
        $(MODEL_BASE)_$(SYM_MODEL)_vent.obj.gz \
	mni_adni_t1w_tal_nlin_asym_ntags_1000_bg.tag.gz \
	mni_adni_t1w_tal_nlin_asym_ntags_1000_nobg.tag.gz \
        mni_adni_hi_t1w_tal_nlin_sym_ntags_nobg.tag.gz \
        mni_adni_hi_t1w_tal_nlin_sym_ntags_bg.tag.gz \
        Cerebellum_Ventricles_SubCortical_Mask-ADNI.mnc.gz \
        Cerebellum_Ventricles_SubCortical_Mask-ADNIhi.mnc.gz \
        gipt_adnihisym.mnc.gz

tag_DATA := \
	mni_adni_t1w_tal_nlin_asym_ntags_1000_bg.tag \
	mni_adni_t1w_tal_nlin_asym_ntags_1000_nobg.tag \
        mni_adni_hi_t1w_tal_nlin_sym_ntags_nobg.tag \
        mni_adni_hi_t1w_tal_nlin_sym_ntags_bg.tag

pve_DATA := \
        gipt_adnihisym.mnc

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
	epm-header.in

m4_files = local_m4/ac_prog_gzip.m4 \
	local_m4/ac_prog_make_model.m4

# be tidy
CLEANFILES = $(pkgdata_DATA) $(tag_DATA) $(pve_DATA) $(MODELS:=.mnc) \
             Cerebellum_Ventricles_SubCortical_Mask-ADNI.mnc \
             Cerebellum_Ventricles_SubCortical_Mask-ADNIhi.mnc

# gunzip rule
%: %.gz
	$(gzip) -d -c $< > $@

all: $(dist_pkgdata_DATA:.gz=) $(DATE)
	for i in $(MODELS); \
	do \
		echo "Doing $$i"; \
      		$(make_model) $$i; \
	done
	for i in $(pkgdata_DATA); \
   	do \
		if [ $${i: -4} == ".mnc" ]; then \
      		echo "Adding mni-model header to $$i"; \
      		minc_modify_header \
			-sinsert mni-model:package=$(PACKAGE) \
			-sinsert mni-model:version=$(VERSION) \
			-sinsert mni-model:compile-date=$(DATE_STAMP) \
			-sinsert mni-model:compile-user=$$USER \
			$$i; \
		fi; \
   	done
