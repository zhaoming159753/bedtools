

<br>
<br>
<br>


<h1>intersectBed</h1>

<b>Note</b>:  <i>When intersecting SNPs, make sure the coordinate conform to the UCSC format.  That is,<br>
the start position for each SNP should be SNP position - 1 and the end position should<br>
be SNP position</i>.<br>
E.g. chr7  10000001        10000002        rs123464<br>
<br>
<ul><li>Report the base-pair overlap between sequence alignments and genes.<br>
</li></ul><blockquote><code>$ intersectBed -a reads.bed -b genes.bed</code>
</blockquote><ul><li>Report whether each alignment overlaps one or more genes.  If not, the alignment is not reported.<br>
</li></ul><blockquote><code>$ intersectBed -a reads.bed -b genes.bed -u</code>
</blockquote><ul><li>Report those alignments that overlap NO genes.  Like "grep -v"<br>
</li></ul><blockquote><code>$ intersectBed -a reads.bed -b genes.bed -v</code>
</blockquote><ul><li>Report the number of genes that each alignment overlaps.<br>
</li></ul><blockquote><code>$ intersectBed -a reads.bed -b genes.bed -c</code>
</blockquote><ul><li>Report the entire, original alignment entry for each overlap with a gene.<br>
</li></ul><blockquote><code>$ intersectBed -a reads.bed -b genes.bed -wa</code>
</blockquote><ul><li>Report the entire, original gene entry for each overlap with a gene.<br>
</li></ul><blockquote><code>$ intersectBed -a reads.bed -b genes.bed -wb</code>
</blockquote><ul><li>Report the entire, original alignment and gene entries for each overlap.<br>
</li></ul><blockquote><code>$ intersectBed -a reads.bed -b genes.bed –wa -wb</code>
</blockquote><ul><li>Only report an overlap with a repeat if it spans at least 50% of the exon.<br>
</li></ul><blockquote><code>$ intersectBed -a exons.bed -b repeatMasker.bed –f 0.50</code>
</blockquote><ul><li>Only report an overlap if comprises 50% of the structural variant and 50% of the segmental duplication.  Thus, it is reciprocally at least a 50% overlap.<br>
</li></ul><blockquote><code>$ intersectBed -a SV.bed -b segmentalDups.bed –f 0.50 -r</code>
</blockquote><ul><li>Read BED A from stdin.  For example, find genes that overlap LINEs but not SINEs.<br>
</li></ul><blockquote><code>$ intersectBed -a genes.bed -b LINES.bed | intersectBed -a stdin -b SINEs.bed -v</code>
</blockquote><ul><li>Retain only single-end BAM alignments that overlap exons.<br>
</li></ul><blockquote><code>$ intersectBed -abam reads.bam -b exons.bed &gt; reads.touchingExons.bam</code>
</blockquote><ul><li>Retain only single-end BAM alignments that do not overlap simple sequence repeats.<br>
</li></ul><blockquote><code>$ intersectBed -abam reads.bam -b SSRs.bed -v &gt; reads.noSSRs.bam</code>
</blockquote><ul><li>Retain only paired-end BAM alignments where neither end overlaps simple sequence repeats.</li></ul>


<br><br>


<h1>pairToBed</h1>

<ul><li>Return all structural variants (in BEDPE format) that overlap with genes on either end.<br>
</li></ul><blockquote><code>$ pairToBed -a sv.bedpe -b genes &gt; sv.genes</code>
</blockquote><ul><li>Return all structural variants (in BEDPE format) that overlap with genes on both end.<br>
</li></ul><blockquote><code>$ pairToBed -a sv.bedpe -b genes -type both &gt; sv.genes</code>
</blockquote><ul><li>Retain only paired-end BAM alignments where neither end overlaps simple sequence repeats.<br>
</li></ul><blockquote><code>$ pairToBed -abam reads.bam -b SSRs.bed -type neither &gt; reads.noSSRs.bam</code>
</blockquote><ul><li>Retain only paired-end BAM alignments where both ends overlap segmental duplications.<br>
</li></ul><blockquote><code>$ pairToBed -abam reads.bam -b segdups.bed -type both &gt; reads.SSRs.bam</code>
</blockquote><ul><li>Retain only paired-end BAM alignments where neither or one and only one end overlaps segmental duplications.<br>
</li></ul><blockquote><code>$ pairToBed -abam reads.bam -b segdups.bed -type notboth &gt; reads.notbothSSRs.bam</code></blockquote>



<br><br>



<h1>pairToPair</h1>

<ul><li>Find all SVs (in BEDPE format) in sample 1 that are also in sample 2.<br>
</li></ul><blockquote><code>$ pairToPair -a 1.sv.bedpe -b 2.sv.bedpe | cut -f 1-10 &gt; 1.sv.in2.bedpe</code></blockquote>

<ul><li>Find all SVs (in BEDPE format) in sample 1 that are not in sample 2.<br>
</li></ul><blockquote><code>pairToPair -a 1.sv.bedpe -b 2.sv.bedpe -type neither | cut -f 1-10 &gt; 1.sv.notin2.bedpe</code></blockquote>



<br><br>



<h1>bamToBed</h1>
<ul><li>Convert BAM alignments to BED format.<br>
</li></ul><blockquote><code>$ bamToBed -i reads.bam &gt; reads.bed</code>
</blockquote><ul><li>Convert BAM alignments to BED format using edit distance (NM) as the BED “score”.<br>
</li></ul><blockquote><code>$ bamToBed -i reads.bam -ed &gt; reads.bed</code>
</blockquote><ul><li>Convert BAM alignments to BEDPE format.<br>
</li></ul><blockquote><code>$ bamToBed -i reads.bam -bedpe &gt; reads.bedpe</code></blockquote>



<br><br>



<h1>windowBed</h1>

<ul><li>Report all genes that are within 10000 bp upstream or downstream of CNVs.<br>
</li></ul><blockquote><code>$ windowBed -a CNVs.bed -b genes.bed -w 10000</code></blockquote>

<ul><li>Report all genes that are within 10000 bp upstream or 5000 bp downstream of CNVs.<br>
</li></ul><blockquote><code>$ windowBed -a CNVs.bed -b genes.bed –l 10000 –r 5000</code></blockquote>

<ul><li>Report all SNPs that are within 5000 bp upstream or 1000 bp downstream of genes. Define upstream and downstream based on strand.<br>
</li></ul><blockquote><code>$ windowBed -a genes.bed –b snps.bed –l 5000 –r 1000 -sw</code></blockquote>



<br><br>



<h1>closestBed</h1>

<b>Note:</b> <i>By default, if there is a tie for closest, all ties will be reported. closestBed allows overlapping features to be the closest.</i>

<ul><li>Find the closest ALU to each gene.<br>
</li></ul><blockquote><code>$ closestBed -a genes.bed -b ALUs.bed</code></blockquote>

<ul><li>Find the closest ALU to each gene, choosing the first ALU in the file if there is a tie.<br>
</li></ul><blockquote><code>$ closestBed -a genes.bed -b ALUs.bed –t first</code></blockquote>

<ul><li>Find the closest ALU to each gene, choosing the last ALU in the file if there is a tie.<br>
</li></ul><blockquote><code>$ closestBed -a genes.bed -b ALUs.bed –t last</code></blockquote>



<br><br>



<h1>subtractBed</h1>

<b>Note:</b> <i>If a feature in A is entirely "spanned" by any feature in B, it will not be reported.</i>

<ul><li>Remove introns from gene features.  Exons will (should) be reported.<br>
</li></ul><blockquote><code>$ subtractBed -a genes.bed -b introns.bed</code></blockquote>



<br><br>



<h1>mergeBed</h1>

<ul><li>Merge overlapping repetitive elements into a single entry.<br>
</li></ul><blockquote><code>$ mergeBed -i repeatMasker.bed</code></blockquote>

<ul><li>Merge overlapping repetitive elements into a single entry, returning the number of entries merged.<br>
</li></ul><blockquote><code>$ mergeBed -i repeatMasker.bed -n</code></blockquote>

<ul><li>Merge nearby (within 1000 bp) repetitive elements into a single entry.<br>
</li></ul><blockquote><code>$ mergeBed -i repeatMasker.bed -d 1000</code></blockquote>



<br><br>



<h1>coverageBed</h1>

<ul><li>Compute the coverage of aligned sequences on 10 kilobase “windows” spanning the genome.<br>
</li></ul><blockquote><code>$ coverageBed -a reads.bed -b windows10kb.bed | head</code></blockquote>

<ul><li>Compute the coverage of aligned sequences on 10 kilobase “windows” spanning the genome and created a BEDGRAPH of the number of aligned reads in each window for display on the UCSC browser.<br>
</li></ul><blockquote><code>$ coverageBed -a reads.bed -b windows10kb.bed | cut –f 1-4 &gt; windows10kb.cov.bedg</code>
</blockquote><ul><li>Compute the coverage of aligned sequences on 10 kilobase “windows” spanning the genome and created a BEDGRAPH of the fraction of each window covered by at least one aligned read for display on the UCSC browser.<br>
</li></ul><blockquote><code>$ coverageBed -a reads.bed -b windows10kb.bed | awk ‘{OFS=”\t”; print $1,$2,$3,$6}’ &gt; windows10kb.pctcov.bedg</code></blockquote>


<br><br>



<h1>complementBed</h1>

<ul><li>Report all intervals in the human genome that are not covered by repetitive elements.<br>
</li></ul><blockquote><code>$ complementBed -i repeatMasker.bed -g hg18.genome</code></blockquote>


<br><br>



<h1>shuffleBed</h1>

<ul><li>Randomly place all discovered variants in the genome.  However, prevent them from being placed in know genome gaps.<br>
</li></ul><blockquote><code>$ shuffleBed -i variants.bed -g hg18.genome -excl genome_gaps.bed</code></blockquote>


<ul><li>Randomly place all discovered variants in the genome.  However, prevent them from being placed in know genome gaps and require that the variants be randomly placed on the same chromosome.<br>
</li></ul><blockquote><code>$ shuffleBed -i variants.bed -g hg18.genome -excl genome_gaps.bed -chrom</code></blockquote>


<h1>groupBy</h1>

<b>Note</b> groupBy assumes the input data are sorted by the grouping columns you will use.  This is typically true for output from all BEDTools.<br>
<br>
Let's imagine we have three incredibly intriguing genetic variants that we are studying.<br>
<br>
<pre><code>$ cat variants.bed<br>
chr21	9719758	9729320	variant1<br>
chr21	9729310	9757478	variant2<br>
chr21   9795588 9796685 variant3<br>
</code></pre>

We are interested in what repeats these variants overlap with in our genome, so we use intersectedBed.<br>
<br>
<pre><code>$ intersectBed -a variants.bed -b repeats.bed -wa -wb &gt; variantsToRepeats.bed<br>
$ cat variantsToRepeats.bed<br>
chr21	9719758	9729320	variant1	chr21	9719768	9721892	ALR/Alpha	1004	+<br>
chr21	9719758	9729320	variant1	chr21	9721905	9725582	ALR/Alpha	1010	+<br>
chr21	9719758	9729320	variant1	chr21	9725582	9725977	L1PA3	3288	+<br>
chr21	9719758	9729320	variant1	chr21	9726021	9729309	ALR/Alpha	1051	+<br>
chr21	9729310	9757478	variant2	chr21	9729320	9729809	L1PA3	3897	-<br>
chr21	9729310	9757478	variant2	chr21	9729809	9730866	L1P1	8367	+<br>
chr21	9729310	9757478	variant2	chr21	9730866	9734026	ALR/Alpha	1036	-<br>
chr21	9729310	9757478	variant2	chr21	9734037	9757471	ALR/Alpha	1182	-<br>
chr21	9795588	9796685	variant3	chr21	9795589	9795713	(GAATG)n	308	+<br>
chr21	9795588	9796685	variant3	chr21	9795736	9795894	(GAATG)n	683	+<br>
chr21	9795588	9796685	variant3	chr21	9795911	9796007	(GAATG)n	345	+<br>
chr21	9795588	9796685	variant3	chr21	9796028	9796187	(GAATG)n	756	+<br>
chr21	9795588	9796685	variant3	chr21	9796202	9796615	(GAATG)n	891	+<br>
chr21	9795588	9796685	variant3	chr21	9796637	9796824	(GAATG)n	621	+<br>
</code></pre>

We can see that variant1 overlaps with 3 repeats, variant2 with 4 and variant3 with 6.  We can use groupBy to summarize the hits for each variant in several useful ways.<br>
<br>
First, let's find the min and max repeat score for each variant.  We do this by "grouping" on the variant coordinate columns (i.e. cols. 1,2 and 3) and ask for the min and max of the repeat score column (i.e. col. 9).<br>
<br>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 1,2,3 -opCol 9 -op min<br>
chr21	9719758	9729320	1004<br>
chr21	9729310	9757478	1036<br>
chr21	9795588	9796685	308<br>
</code></pre>

We can also group on just the name column with similar effect.<br>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 4 -opCol 9 -op min<br>
variant1	1004<br>
variant2	1036<br>
variant3	308<br>
</code></pre>

What about the <b>max</b> score?  Let's keep the coordinates and the name of the variants so that we stay in BED format.<br>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 1,2,3,4 -opCol 9 -op max<br>
chr21	9719758	9729320	variant1	3288<br>
chr21	9729310	9757478	variant2	8367<br>
chr21	9795588	9796685	variant3	891<br>
</code></pre>

The mean score?<br>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 1,2,3,4 -opCol 9 -op mean<br>
chr21	9719758	9729320	variant1	1588.25<br>
chr21	9729310	9757478	variant2	3620.5<br>
chr21	9795588	9796685	variant3	600.6667<br>
</code></pre>

The median score? You get the point...<br>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 1,2,3,4 -opCol 9 -op median<br>
chr21	9719758	9729320	variant1	1030.5<br>
chr21	9729310	9757478	variant2	2539.5<br>
chr21	9795588	9796685	variant3	652<br>
</code></pre>


What is the <b>most common</b> repeat name overlapped?<br>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 1,2,3,4 -opCol 8 -op mode<br>
chr21	9719758	9729320	variant1	ALR/Alpha<br>
chr21	9729310	9757478	variant2	ALR/Alpha<br>
chr21	9795588	9796685	variant3	(GAATG)n<br>
</code></pre>

<b>Least common?</b>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 1,2,3,4 -opCol 8 -op antimode<br>
chr21	9719758	9729320	variant1	L1PA3<br>
chr21	9729310	9757478	variant2	L1P1<br>
chr21	9795588	9796685	variant3	(GAATG)n<br>
</code></pre>

Now for something different.  What if we wanted all of the names of the repeats listed on the same line as the variants?  Use the collapse option.  This "denormalizes" things.<br>
<pre><code>$ groupBy -i variantsToRepeats.bed -grp 1,2,3,4 -opCol 8 -op collapse<br>
chr21	9719758	9729320	variant1	ALR/Alpha,ALR/Alpha,L1PA3,ALR/Alpha,<br>
chr21	9729310	9757478	variant2	L1PA3,L1P1,ALR/Alpha,ALR/Alpha,<br>
chr21	9795588	9796685	variant3	(GAATG)n,(GAATG)n,(GAATG)n,(GAATG)n,(GAATG)n,(GAATG)n,<br>
</code></pre>