<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgheadline2">GTAGS</a>
<ul>
<li><a href="#orgheadline1">.globalrc</a></li>
</ul>
</li>
<li><a href="#orgheadline4">.globalrc</a>
<ul>
<li><a href="#orgheadline3">.ctagsrc</a></li>
</ul>
</li>
</ul>
</div>
</div>

# GTAGS<a id="orgheadline2"></a>

## .globalrc<a id="orgheadline1"></a>

    --regex-ruby=/(^|[:;])[ \t]*([A-Z][[:alnum:]_]+) *=/\2/c,class,constant/
    --regex-ruby=/(^|;)[ \t]*(has_many|belongs_to|has_one|has_and_belongs_to_many)\(? *:([[:alnum:]_]+)/\3/f,function,association/
    --regex-ruby=/(^|;)[ \t]*(named_)?scope\(? *:([[:alnum:]_]+)/\3/f,function,named_scope/
    --regex-ruby=/(^|;)[ \t]*expose\(? *:([[:alnum:]_]+)/\2/f,function,exposure/
    --regex-ruby=/(^|;)[ \t]*event\(? *:([[:alnum:]_]+)/\2/f,function,aasm_event/
    --regex-ruby=/(^|;)[ \t]*event\(? *:([[:alnum:]_]+)/\2!/f,function,aasm_event/
    --regex-ruby=/(^|;)[ \t]*event\(? *:([[:alnum:]_]+)/\2?/f,function,aasm_event/

    --regex-JavaScript=/([A-Za-z0-9._$]+)[ \t]*[:=][ \t]*\{/\1/,object/
    --regex-JavaScript=/([A-Za-z0-9._$()]+)[ \t]*[:=][ \t]*function[ \t]*\(/\1/,function/
    --regex-JavaScript=/([A-Za-z0-9._$()]+)[ \t]*[:=][ \t]*\(function[ \t]*\(\)/\1/,function/
    --regex-JavaScript=/function[ \t]+([A-Za-z0-9._$]+)[ \t]*\(([^)])\)/\1/,function/
    --regex-JavaScript=/([A-Za-z0-9._$]+)[ \t]*[:=][ \t]*\[/\1/,array/
    --regex-JavaScript=/([^= ]+)[ \t]*=[ \t]*[^"]'[^']*/\1/,string/
    --regex-JavaScript=/Handlebars\.registerHelper\(['"]([A-Za-z0-9._$]+)['"]/\1/,string/
    --regex-JavaScript=/var\s+([A-Za-z0-9._$]+)\s+=\s+_.bind\(/\1/,string/
    --regex-JavaScript=/var\s+([A-Za-z0-9._$]+)\s+=\s+\(\s+function\s+\(\)/\1/,variable/
    --regex-JavaScript=/var\s+([A-Za-z0-9._$]+)\s+=/\1/,variable/

    --langdef=coffee
    --langmap=coffee:.coffee
    --regex-coffee=/^[ \t]*([A-Za-z.]+)[ \t]+=.*->.*$/\1/f,function/
    --regex-coffee=/^[ \t]*([A-Za-z.]+)[ \t]+=[^->\n]*$/\1/v,variable/
    --regex-coffee=/^[ \t]*((class ){1}[A-Za-z.]+)[ \t]+=[^->\n]*$/\1/v,object/

    --exclude=jquery.js
    --exclude=modernizr.js
    --exclude=custom.modernizr.js
    --exclude=underscore-min.js
    --exclude=underscore.js
    --exclude=nwmatcher-1.2.5-min.js
    --exclude=rem.js
    --exclude=jsmock.js
    --exclude=*.min.js
    --exclude=window_min.js
    --exclude=jquery-1.9.1-min.js
    --exclude=jquery-1.9.1.js
    --exclude=underscore.string.js
    --exclude=json2.js
    --exclude=datepicker.js
    --exclude=datepicker.packed.js
    --exclude=query.datetimepicker.js

# .globalrc<a id="orgheadline4"></a>

    default:\
      :tc=exuberant-ctags:tc=htags:
    #---------------------------------------------------------------------
    # Configuration for gtags(1)
    # See gtags(1).
    #---------------------------------------------------------------------

    common:\
      :skip=spec_lib/,spec/,tmp/,db/,java/,test/,test_extensions/,HTML/,HTML.pub/,tags,TAGS,ID,y.tab.c,y.tab.h,cscope.out,cscope.po.out,cscope.in.out,SCCS/,RCS/,CVS/,CVSROOT/,{arch}/,autom4te.cache/:
    gtags:\
      :tc=common:\
      :langmap=c\:.c.h,yacc\:.y,asm\:.s.S,java\:.java,cpp\:.c++.cc.cpp.cxx.hxx.hpp.C.H.inl,php\:.php.php3.phtml:
    #
    # plug-in parser (for Exuberant Ctags 5.8)
    #
    exuberant-ctags|plugin-example|Example of function layer plugin parser:\
      :tc=common:\
      :langmap=Asm\:.asm.ASM.s.S:\
      :langmap=Asp\:.asp.asa:\
      :langmap=Awk\:.awk.gawk.mawk:\
      :langmap=Basic\:.bas.bi.bb.pb:\
      :langmap=BETA\:.bet:\
      :langmap=C\:.c:\
      :langmap=C++\:.c++.cc.cp.cpp.cxx.h.h++.hh.hp.hpp.hxx.C.H.inl:\
      :langmap=C#\:.cs:\
      :langmap=Cobol\:.cbl.cob.CBL.COB:\
      :langmap=DosBatch\:.bat.cmd:\
      :langmap=Eiffel\:.e:\
      :langmap=Erlang\:.erl.ERL.hrl.HRL:\
      :langmap=Flex\:.as.mxml:\
      :langmap=Fortran\:.f.for.ftn.f77.f90.f95.F.FOR.FTN.F77.F90.F95:\
      :langmap=HTML\:.htm.html.hbs:\
      :langmap=Java\:.java:\
      :langmap=JavaScript\:.js:\
      :langmap=Lisp\:.cl.clisp.el.l.lisp.lsp:\
      :langmap=Lua\:.lua:\
      :langmap=MatLab\:.m:\
      :langmap=OCaml\:.ml.mli:\
      :langmap=Pascal\:.p.pas:\
      :langmap=Perl\:.pl.pm.plx.perl:\
      :langmap=PHP\:.php.php3.phtml:\
      :langmap=Python\:.py.pyx.pxd.pxi.scons:\
      :langmap=REXX\:.cmd.rexx.rx:\
      :langmap=Ruby\:.rb.ruby:\
      :langmap=Scheme\:.SCM.SM.sch.scheme.scm.sm:\
      :langmap=Sh\:.sh.SH.bsh.bash.ksh.zsh:\
      :langmap=SLang\:.sl:\
      :langmap=SML\:.sml.sig:\
      :langmap=SQL\:.sql:\
      :langmap=Tcl\:.tcl.tk.wish.itcl:\
      :langmap=Tex\:.tex:\
      :langmap=Vera\:.vr.vri.vrh:\
      :langmap=Verilog\:.v:\
      :langmap=VHDL\:.vhdl.vhd:\
      :langmap=Vim\:.vim:\
      :langmap=YACC\:.y:\
      :gtags_parser=Asm\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Asp\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Awk\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Basic\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=BETA\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=C\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=C++\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=C#\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Cobol\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=DosBatch\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Eiffel\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Erlang\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Flex\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Fortran\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=HTML\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Java\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=JavaScript\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Lisp\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Lua\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=MatLab\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=OCaml\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Pascal\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Perl\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=PHP\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Python\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=REXX\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Ruby\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Scheme\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Sh\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=SLang\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=SML\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=SQL\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Tcl\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Tex\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Vera\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Verilog\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=VHDL\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=Vim\:/usr/local/lib/gtags/exuberant-ctags.la:\
      :gtags_parser=YACC\:/usr/local/lib/gtags/exuberant-ctags.la:

    ctags:\
      :tc=exuberant-ctags:


    #---------------------------------------------------------------------
    # Configuration for htags(1)
    # Let's paint hypertext with your favorite colors!
    # See htags(1).
    #---------------------------------------------------------------------
    htags:\
      :body_begin=<body text='#191970' bgcolor='#f5f5dc' vlink='gray'>:body_end=</body>:\
      :table_begin=<table>:table_end=</table>:\
      :title_begin=<h1><font color='#cc0000'>:title_end=</font></h1>:\
      :comment_begin=<i><font color='green'>:comment_end=</font></i>:\
      :sharp_begin=<font color='darkred'>:sharp_end=</font>:\
      :brace_begin=<font color='red'>:brace_end=</font>:\
      :warned_line_begin=<span style='background-color\:yellow'>:warned_line_end=</span>:\
      :reserved_begin=<b>:reserved_end=</b>:script_alias=/cgi-bin/:\
      :ncol#4:tabs#8:normal_suffix=html:gzipped_suffix=ghtml:

## .ctagsrc<a id="orgheadline3"></a>
