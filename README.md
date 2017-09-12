# Ellingrod_AAP
##9/11/17
###Not completed

##Below are the mothur commands use to process the sequences

make.contigs(file=uic_7.files, processors=10)

summary.seqs(fasta=current)

screen.seqs(fasta=current, group=current, summary=current, maxambig=0, maxlength=275)

summary.seqs(fasta=current)

get.current()

###proccesing improved sequences

unique.seqs(fasta=uic.trim.contigs.good.pick.fasta)

count.seqs(name=uic.trim.contigs.good.names, group=uic.contigs.good.pick.groups)

summary.seqs(count=current)

align.seqs(fasta=current, reference=silva.v4.fasta)

get.current()

summary.seqs(fasta=uic.trim.contigs.good.pick.unique.align, count=uic.trim.contigs.good.count_table)
screen.seqs(fasta=current, count=current, summary=current, start=1968, end=11550, maxhomop=8)
summary.seqs(fasta=current, count=current)
filter.seqs(fasta=current, vertical=T, trump=.)
get.current()
unique.seqs(fasta=current, count=current)
pre.cluster(fasta=current, count=current, diffs=2)
get.current()
chimera.uchime(fasta=current, count=current)
remove.seqs(count=current, accnos=current)
summary.seqs(fasta=current, count=current)
classify.seqs(fasta=uic.trim.contigs.good.pick.unique.good.filter.unique.precluster.pick.fasta, count=uic.trim.contigs.good.pick.unique.good.filter.unique.precluster.pick.count_table, reference=trainset14_032015.rdp.fasta, taxonomy=trainset14_032015.rdp.tax, cutoff=80)
remove.lineage(fasta=current, count=current, taxonomy=current, taxon=Chloroplast-Mitochondria-unknown-Archaea-Eukaryota)
summary.tax(taxonomy=current, count=current)
get.current()

###Preparing for analysis
remove.groups(count=uic.trim.contigs.good.pick.unique.good.filter.unique.precluster.pick.pick.count_table, taxonomy=uic.trim.contigs.good.pick.unique.good.filter.unique.precluster.pick.rdp.wang.pick.taxonomy, fasta=uic.trim.contigs.good.pick.unique.good.filter.unique.precluster.pick.pick.fasta, groups=mockD)
cluster.split(fasta=current, count=current, taxonomy=current, splitmethod=classify, taxlevel=4, cutoff=0.03)
get.current()
make.shared(list=current, count=current, label=0.03)
classify.otu(list=current, count=current, taxonomy=current, label=0.03)
rename.file(count=current, shared=current, constaxonomy=current)
count.groups(shared=current)
get.current()
sub.sample(shared=current, size=2500)
rarefaction.single(shared=uic.opti_mcc.shared, calc=sobs, freq=100)
summary.single(shared=uic.opti_mcc.shared, calc=nseqs-coverage-sobs-invsimpson, subsample=2392)


### in R, I averaged all the OTU values for the biological replicates for each ID. - see R code for aggregating shared file per ID
## the new shared file created with this code was mod5.opti_mcc.shared
dist.shared(shared=mod5.opti_mcc.shared, calc=thetayc-jclass, subsample=2500)
pcoa(phylip=mod5.opti_mcc.thetayc.0.03.lt.ave.dist)
nmds(phylip=mod5.opti_mcc.thetayc.0.03.lt.ave.dist, mindim=3, maxdim=3)

