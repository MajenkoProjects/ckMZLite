SCHEMATICS = ckMZLite.sch
PROJECT = ckMZLite

export: $(PROJECT).pdf

$(PROJECT).pdf: $(SCHEMATICS)
	gaf export -o $@ $^

gerber: $(PROJECT).pcb
	mkdir -p Gerber
	pcb -x gerber --metric --gerberfile "Gerber/$(PROJECT)" $(PROJECT).pcb
	pcb -x bom --bomfile "Gerber/$(PROJECT).bom" --xyfile "Gerber/$(PROJECT).xy" "$(PROJECT).pcb";
	if [ -f "Gerber/$(PROJECT).top.gbr" ]; then mv "Gerber/$(PROJECT).top.gbr" "Gerber/$(PROJECT).GTL"; fi
	if [ -f "Gerber/$(PROJECT).group1.gbr" ]; then mv "Gerber/$(PROJECT).group1.gbr" "Gerber/$(PROJECT).GL2"; fi
	if [ -f "Gerber/$(PROJECT).group2.gbr" ]; then mv "Gerber/$(PROJECT).group2.gbr" "Gerber/$(PROJECT).GL3"; fi
	if [ -f "Gerber/$(PROJECT).bottom.gbr" ]; then mv "Gerber/$(PROJECT).bottom.gbr" "Gerber/$(PROJECT).GBL"; fi
	if [ -f "Gerber/$(PROJECT).topmask.gbr" ]; then mv "Gerber/$(PROJECT).topmask.gbr" "Gerber/$(PROJECT).GTS"; fi
	if [ -f "Gerber/$(PROJECT).bottommask.gbr" ]; then mv "Gerber/$(PROJECT).bottommask.gbr" "Gerber/$(PROJECT).GBS"; fi
	if [ -f "Gerber/$(PROJECT).topsilk.gbr" ]; then mv "Gerber/$(PROJECT).topsilk.gbr" "Gerber/$(PROJECT).GTO"; fi
	if [ -f "Gerber/$(PROJECT).bottomsilk.gbr" ]; then mv "Gerber/$(PROJECT).bottomsilk.gbr" "Gerber/$(PROJECT).GBO"; fi
	if [ -f "Gerber/$(PROJECT).plated-drill.cnc" ]; then mv "Gerber/$(PROJECT).plated-drill.cnc" "Gerber/$(PROJECT).TXT"; fi
	if [ -f "Gerber/$(PROJECT).outline.gbr" ]; then mv "Gerber/$(PROJECT).outline.gbr" "Gerber/$(PROJECT).GML"; fi

render: $(PROJECT).pcb
	mkdir -p Render
	pcb -x gerber --metric --gerberfile "Render/$(PROJECT)" $(PROJECT).pcb
	pcb -x bom --bomfile "Render/$(PROJECT).bom" --xyfile "Render/$(PROJECT).xy" "$(PROJECT).pcb"
	cd Render && gentex -n $(PROJECT)
