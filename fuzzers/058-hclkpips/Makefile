
N := 2
SPECIMENS := $(addprefix specimen_,$(shell seq -f '%03.0f' $(N)))
SPECIMENS_OK := $(addsuffix /OK,$(SPECIMENS))

database: $(SPECIMENS_OK)
	${XRAY_SEGMATCH} -o seg_hclk_l.segbits $(addsuffix /segdata_hclk_l_design_*.txt,$(SPECIMENS))
	${XRAY_SEGMATCH} -o seg_hclk_r.segbits $(addsuffix /segdata_hclk_r_design_*.txt,$(SPECIMENS))

pushdb:
	${XRAY_MERGEDB} hclk_l seg_hclk_l.segbits
	${XRAY_MERGEDB} hclk_r seg_hclk_r.segbits
	${XRAY_DBFIXUP}

$(SPECIMENS_OK):
	bash generate.sh $(subst /OK,,$@)
	touch $@

clean:
	rm -rf specimen_[0-9][0-9][0-9]/ seg_hclk_[lr].segbits

.PHONY: database pushdb clean
