

# Introduction #

Below are common questions that are commonly asked by new BEDTools users. We have attempted to organize the content by subject.

<br>


<h2>Problems compiling BEDTools</h2>
<blockquote><h3>What are all of these zlib errors?</h3>
BEDTools supports BAM and gzipped BED/GFF/VCF files through use of the zlib libraries. Some versions of Ubuntu and other UNIX flavors come without the zlib libraries installed.  If you run into this, please try first installing the zlib libraries.  For example, on Ubuntu, this would be:<br>
<pre><code>sudo apt-get install zlib<br>
sudo apt-get install zlib-devel<br>
</code></pre></blockquote>

<h2>Problems with running BEDTools commands</h2>
<blockquote><h3>How do I see the help for a given command?</h3>
All BEDTools commands have a "-h" option.  Additionally, some tools will provide the help menu if you just type the command line followed by enter.<br>
<pre><code>$ coverageBed -h<br>
<br>
Program: coverageBed (v2.11.2)<br>
Author:  Aaron Quinlan (aaronquinlan@gmail.com)<br>
Summary: Returns the depth and breadth of coverage of features from A<br>
	 on the intervals in B.<br>
<br>
Usage:   coverageBed [OPTIONS] -a &lt;bed/gff/vcf&gt; -b &lt;bed/gff/vcf&gt;<br>
<br>
Options: <br>
	-abam	The A input file is in BAM format.<br>
<br>
	-s	Force strandedness.  That is, only include hits in A that<br>
		overlap B on the same strand.<br>
		- By default, hits are included without respect to strand.<br>
...<br>
</code></pre></blockquote>

<br>

<h2>Problems with file formats</h2>


<blockquote><h3>What does zero-based, half-open mean?</h3>
BEDTools users are sometimes confused by the way BED start and end coordinates are represented. BEDTools uses the UCSC Genome Browser’s internal database convention of making the start position 0-based and the end position 1-based: (<a href='http://genome.ucsc.edu/FAQ/FAQtracks#tracks1'>http://genome.ucsc.edu/FAQ/FAQtracks#tracks1</a>). In other words, BEDTools interprets the “start” column as being 1 basepair higher than what is represented in the file. For example, the following BED feature represents a single base on chromosome 1; namely, the 1st base.<br>
<pre><code>$ cat first_base.bed <br>
chr1	0	1	i-am-the-first-position-on-chrom1<br>
</code></pre>
Why, you might ask? The advantage of storing features this way is that it prevents lots of superfluous "+1" operations in the code when computing lengths, overlap, etc. These would be necessary were the coordinate system 1-based, inclusive. Thus, storing BED features this way reduces the computational burden.</blockquote>

<br>

<blockquote><h3>Why must my input files be tab-delimited?</h3>
While it is certainly possible to allow BED and other formats to be delimited by any form of whitespace, we have decided to require tab delimiters for three reasons:<br>
<ol><li>By requiring one delimiter type, the processing time is minimized.<br>
</li><li>Tab-delimited files are more amenable to other UNIX utilities.<br>
</li><li>GFF files can contain spaces within attribute columns. This complicates the use of space-delimited files as spaces must therefore be treated specially depending on the context.</li></ol></blockquote>

<br>

<blockquote><h3>Why do I get the "It looks as though you have less than 3 columns at line: 1." message?</h3>
This is typically caused by files that use a delimiter other than TAB.</blockquote>

<br>

<h2>Problems with output</h2>

<br>


<h2>Converting among formats</h2>

<br>

<h2>Miscellaneous</h2>
<blockquote><h3>What happened to the "groupBy" tool?</h3>
In the interest of keeping the software we develop in logical collections, groupBy has been moved to the <a href='https://github.com/arq5x/filo'>filo</a> project.