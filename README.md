Gendermix: Gender inference from genotype array data
====================================================

Author: Iain Bancarz, ib5@sanger.ac.uk


1. Introduction
---------------

Inference of sample gender is used as a quality control measure for
genotyping array data, at the Wellcome Trust Sanger Institute (WTSI) and 
elsewhere. Gender can be inferred from heterozygosity on the X chromosome 
(xhet), and compared to the known gender of the sample to detect sample
swaps and other potential issues.

Xhet is expected to be zero for male samples, and non-zero for females. We
need to set thresholds M_max and F_min, respectively for the maximum xhet on
male samples and minimum xhet on female samples. (If xhet for a given sample
is too high for male and too low for female, it may be flagged as ambiguous
and marked as a QC failure.)

The xhet can vary considerably between sample sets and SNP arrays. A
single, fixed threshold is not appropriate for all datasets. Instead, we
implement an *adaptive threshold*, which uses machine learning methods to
automatically determine appropriate thresholds from the data.

Gendermix is implemented as a Perl wrapper around an R script. It models the
distribution of genders as a mixture (weighted sum) of two normal
distributions. It attempts to fit this model to the data and determine
appropriate thresholds. In some cases, such as a sample set containing only
one gender, this may not be possible. Therefore, Gendermix applies sanity
checks to its model, and warns the user if the checks fail.


2. Prerequisites
----------------

Software:

* R >= 2.11.1
* R mixtools library: http://cran.r-project.org/web/packages/mixtools/index.html
* Perl >= v5.8.8
* perl-dnap-utilities >= 0.4.1: https://github.com/wtsi-npg/perl-dnap-utilities
* Gftools: https://github.com/wtsi-npg/Gftools


Environment variables:

* PATH       Should include path to <install_dir>/bin
* PERL5LIB   Should include path to <install_dir>/src/perl/lib/
* R_LIBS     Should include path to mixtools library installation


3. Installation
---------------

make install <installation_dir>


4. Usage
--------

Gendermix may be run from within Perl code using the Gendermix.pm module, or
from the command line using the check_xhet_gender.pl or gendermix.pl scripts.
See documentation in the individual modules and scripts for details.


5. History
----------

Gendermix was initially implemented as part of the WTSI genotyping pipeline.
It was moved into a separate Github repository on 3 December 2014. Commit
history prior to that date can be viewed in the WTSI genotyping
repository: https://github.com/wtsi-npg/genotyping


6. License statement
--------------------

Copyright (C) 2012 - 2014 Genome Research Ltd.

Author: Iain Bancarz, ib5@sanger.ac.uk

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.