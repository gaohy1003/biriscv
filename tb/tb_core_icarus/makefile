all:comp elab sim
#--------------------------------------------------------
export VERDI_HOME=/nfs/tools/synopsys/verdi/R-2020.12-SP1
vlogan_opts=-full64 -v2005  +define+TRACE

vcs_elab_opts=-full64 -debug_pp -t ps -licqueue -l elaborate.log -P ${VERDI_HOME}/share/PLI/VCS/LINUX64/novas.tab ${VERDI_HOME}/share/PLI/VCS/LINUX64/pli.a
vcs_sim_opts=-ucli -licqueue -l sim.log
top=top
simfile = ./filelist.f

comp:
	vlogan ${vlogan_opts} +v2k -sverilog \
	+incdir+./../../src/core \
	-f $(simfile) \
	-l ./vlogan.log \
	
elab:
	vcs ${vcs_elab_opts} work.tb_${top} -o tb_${top}_simv \
	-cm line+cond+fsm+branch+tgl \
        -cm_name ${top} \
        -cm_dir ./${top}.vdb
sim:
	./tb_${top}_simv ${vcs_sim_opts} -do simulate.do \
        -cm line+cond+fsm+branch+tgl \
        -cm_name ${top} \
        -cm_dir ./${top}.vdb

verdi_lib:
	vericom -sv +incdir+./../../src/core -f filelist.f
verdi:
	verdi -lib work -top tb_top -ssy -ssv &
clean:
	rm  -rf  *~  core  csrc  *simv  vc_hdrs.h  ucli.key  urg* *.log  novas.* \
        *.fsdb* verdiLog  64* DVEfiles *.vpd *_report *.vdb *.daidir *.vf
