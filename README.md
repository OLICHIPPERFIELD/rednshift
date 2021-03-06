# rednshift for R

Provides a new function that permits the querying of very large datasets (n millions of rows) from redshift.  It's a companion to [pingles redshift](https://github.com/pingles/redshift-r) package which is itself a companion to [Amazon's Redshift](http://aws.amazon.com/redshift/) service for R.

The library contains only one function, redshift_query_n.  

It works by dumping interim files to a nominated AWS bucket, it then sequentially retrieves these data sets from the bucket, rather than a single compiled dataset as is usual for a redshift query. This prevents java overhead errors or excessively long waits for data retrieval. Parallel processing is enabled to speed up the process, but it can executed without parallel processing.

## Installing

You'll need several package dependencies.  Most will be available on CRAN and will install automatically when installing the package.  A few will have to be installed from github.  For this you'll need devtools installed.

    install.packages("devtools")

You'll then need to install redshift.

    devtools::install_github("pingles/redshift-r")

You'll need a developmentment version of [xml2](https://github.com/hadley/xml2) to support [aws.s3](https://github.com/cloudyr/aws.s3):

        devtools::install_github("hadley/xml2")

And now [aws.s3](https://github.com/cloudyr/aws.s3):

latest stable version

    install.packages("aws.s3", repos = c("cloudyr" = "http://cloudyr.github.io/drat"))

on windows you may need:

    install.packages("aws.s3", repos = c("cloudyr" = "http://cloudyr.github.io/drat"), INSTALL_opts = "--no-multiarch")

The last step is to install the rednshift package itself:

    devtools::install_github("oli-chipperfield/rednshift")

## Usage

The help file will give you advice on the usage of the redshift_query_n.

    require(rednshift)
    
    help(redshift_query_n)
    
One important factor to take into account is that you need an AWS bucket available and the relevant environment credentials and AWS role to access it.  Note however that the bucket is a temporary store for the data and the interim files are deleted from the bucket in the "clean up" part of the query execution.

## License

Shamelessly ripped from pingles package

This R package includes the Postgresql JDBC binary which is distributed under the following license:

    Copyright (c) 1997-2011, PostgreSQL Global Development Group
    All rights reserved.

    Redistribution and use in source and binary forms, with or without
    modification, are permitted provided that the following conditions are met:

    1. Redistributions of source code must retain the above copyright notice,
       this list of conditions and the following disclaimer.
    2. Redistributions in binary form must reproduce the above copyright notice,
       this list of conditions and the following disclaimer in the documentation
       and/or other materials provided with the distribution.
    3. Neither the name of the PostgreSQL Global Development Group nor the names
       of its contributors may be used to endorse or promote products derived
       from this software without specific prior written permission.

    THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
    AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
    IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
    ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE
    LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
    CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
    SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
    INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
    CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
    ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
    POSSIBILITY OF SUCH DAMAGE.

This Redshift R code is distributed under the [Eclipse Public License](http://www.eclipse.org/legal/epl-v10.html).
