<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgheadline14">.zshrc</a>
<ul>
<li><a href="#orgheadline1">Load oh-my-zsh</a></li>
<li><a href="#orgheadline2">Use PowerLevel9k Theme</a></li>
<li><a href="#orgheadline3">Oh-my-Zsh config</a></li>
<li><a href="#orgheadline4">PATH</a></li>
<li><a href="#orgheadline5">EDITOR</a></li>
<li><a href="#orgheadline6">SSH</a></li>
<li><a href="#orgheadline7">Percol</a></li>
<li><a href="#orgheadline8">Zsh AutoComplete</a></li>
<li><a href="#orgheadline9">Language</a></li>
<li><a href="#orgheadline10">Terminal Color</a></li>
<li><a href="#orgheadline11">GTAGS</a></li>
<li><a href="#orgheadline12">Aliases</a></li>
<li><a href="#orgheadline13">Custom Functions</a></li>
</ul>
</li>
</ul>
</div>
</div>

# .zshrc<a id="orgheadline14"></a>

## Load oh-my-zsh<a id="orgheadline1"></a>

    # PATH to your oh-my-zsh installation.
    export ZSH=$HOME/.oh-my-zsh

## Use PowerLevel9k Theme<a id="orgheadline2"></a>

    POWERLEVEL9K_MODE='flat'
    ZSH_THEME="powerlevel9k/powerlevel9k"

    POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(os_icon dir vcs)
    POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status rvm)
    POWERLEVEL9K_SHORTEN_DIR_LENGTH=3
    POWERLEVEL9K_SHORTEN_STRATEGY="truncate_middle"
    # enable the vcs segment in general
    POWERLEVEL9K_SHOW_CHANGESET=true
    # # just show the 6 first characters of changeset
    POWERLEVEL9K_CHANGESET_HASH_LENGTH=6
    POWERLEVEL9K_STATUS_VERBOSE=false

## Oh-my-Zsh config<a id="orgheadline3"></a>

    DISABLE_UNTRACKED_FILES_DIRTY="true"
    HIST_STAMPS="mm/dd/yyyy"
    # plugins=(git rails)
    source $ZSH/oh-my-zsh.sh

## PATH<a id="orgheadline4"></a>

    # User configuration
    export PATH=".:/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin:$PATH"
    export PATH="$HOME/.rvm/bin:$PATH" # Add RVM to PATH for scripting
    export MANPATH="/usr/local/man:$MANPATH"

## EDITOR<a id="orgheadline5"></a>

    export ALTERNATE_EDITOR=emacsclient
    export EDITOR=vim
    export VISUAL=vim

## SSH<a id="orgheadline6"></a>

    export SSH_KEY_PATH="~/.ssh/dsa_id"

## Percol<a id="orgheadline7"></a>

    function exists { which $1 &> /dev/null }
    if exists percol; then
        function percol_select_history() {
            local tac
            exists gtac && tac="gtac" || { exists tac && tac="tac" || { tac="tail -r" } }
            BUFFER=$(fc -l -n 1 | eval $tac | percol --match-method regex --query "$LBUFFER")
            CURSOR=$#BUFFER         # move cursor
            zle -R -c               # refresh
        }

        zle -N percol_select_history
        bindkey '^R' percol_select_history
    fi

## Zsh AutoComplete<a id="orgheadline8"></a>

    setopt interactivecomments

    autoload -Uz compinit
    compinit

    autoload -Uz bashcompinit
    bashcompinit

    if [ -d $LOCALDIR/cache ] ; then
        zstyle ':completion:*' use-cache on
        zstyle ':completion:*' cache-path $LOCALDIR/cache/
    fi

      # completion colours
      zstyle ':completion:*' list-colors ${(s.:.)LS_COLORS}

    ### highlight parameters with uncommon names
        zstyle ':completion:*:parameters' \
            list-colors "=[^a-zA-Z]*=$color[red]"

    ### highlight aliases
        zstyle ':completion:*:aliases' \
            list-colors "=*=$color[green]"

    ### highlight the original input.
        zstyle ':completion:*:original' \
            list-colors "=*=$color[red];$color[bold]"

    ### highlight words like 'esac' or 'end'
        zstyle ':completion:*:reserved-words' \
            list-colors "=*=$color[red]"

    ### colorize processlist for 'kill'
        zstyle ':completion:*:*:kill:*:processes' \
            list-colors "=(#b) #([0-9]#) #([^ ]#)*=$color[cyan]=$color[yellow]=$color[green]"

    zstyle ':completion:*' insert-unambiguous true
    zstyle ':completion:*' expand prefix suffix
    zstyle ':completion:*' list-suffixes true
    zstyle ':completion:*' ignore-parents pwd parent ..
    zstyle ':completion:*' remove-all-dups true
    zstyle ':completion:*' special-dirs '..'
    zstyle ':completion:*' ambiguous true
    zstyle ':completion:*' glob true
    zstyle ':completion:*' word true
    zstyle ':completion:*' matcher-list 'm:{[:lower:]}={[:upper:]}' 'r:|[._-]=** r:|=**'
    zstyle ':completion:*' menu select

    #Formatting
    zstyle ':completion:*:descriptions' format $'%{\e[0;31m%}completing %B%d%b%{\e[0m%}'
    zstyle ':completion:*:corrections' format $'%{\e[0;31m%}%d (errors: %e)%}'
    zstyle ':completion:*:messages' format '%d'
    zstyle ':completion:*:warnings' format $'%{\e[0;31m%}No matches for:%{\e[0m%} %d'
    zstyle ':completion:*:corrections' format '%B%d (errors: %e)%b'
    zstyle ':completion:*' format 'completing %d'
    zstyle ':completion:*' format $'%{\e[0;31m%}completing %B%d%b%{\e[0m%}'
    zstyle ':completion:*' group-name ''
    zstyle ':completion:*' verbose true

    zstyle ':completion:*:correct:*' insert-unambiguous true
    zstyle ':completion:*:correct:*' max-errors 2 numeric
    zstyle ':completion:*:correct:*' original true
    zstyle ':completion:*:expand:*' group-order all-expansions expansions

    # remove slash if argument is a directory
    zstyle ':completion:*' squeeze-slashes true

    # history
    zstyle ':completion:*:history-words' stop yes
    zstyle ':completion:*:history-words' remove-all-dups yes
    zstyle ':completion:*:history-words' list false
    zstyle ':completion:*:history-words' menu yes

    # describe options in full
    zstyle ':completion:*:options'         description 'yes'

    # cd directory stack menu
    zstyle ':completion:*:*:cd:*:directory-stack' menu yes select

    # array completion element sorting
    zstyle ':completion:*:*:-subscript-:*' tag-order indexes parameters

    zstyle ':completion::*:(-command-|export):*' fake-parameters ${${${_comps[(I)-value-*]#*,}%%,*}:#-*-}
    zstyle ':completion:*:-tilde-:*' group-order 'named-directories' 'path-directories' 'users' 'expand'

    # approximation
    zstyle ':completion:*' completer _expand _complete _match _approximate
    zstyle ':completion:*:match:*' original only
    zstyle -e ':completion:*:approximate:*' max-errors 'reply=( $(( ($#PREFIX+$#SUFFIX)/3 )) numeric )'

    # ssh, scp, ping, host
    test ! -d "$HOME/.ssh" && mkdir "$HOME/.ssh"
    test ! -f "$HOME/.ssh/known_hosts" && touch "$HOME/.ssh/known_hosts"
    test ! -f "$HOME/.ssh/config" && touch "$HOME/.ssh/config"

    zstyle ':completion:*:(scp|rsync):*' tag-order \
            'hosts:-host hosts:-domain:domain hosts:-ipaddr:IP\ address *'
    zstyle ':completion:*:(scp|rsync):*' group-order \
            users files all-files hosts-domain hosts-host hosts-ipaddr
    zstyle ':completion:*:ssh:*' tag-order \
            users 'hosts:-host hosts:-domain:domain hosts:-ipaddr:IP\ address *'
    zstyle ':completion:*:ssh:*' group-order \
            hosts-domain hosts-host users hosts-ipaddr

    zstyle ':completion:*:(ssh|scp|rsync):*:hosts-host' ignored-patterns \
            '*.*' loopback localhost
    zstyle ':completion:*:(ssh|scp|rsync):*:hosts-domain' ignored-patterns \
            '<->.<->.<->.<->' '^*.*' '*@*'
    zstyle ':completion:*:(ssh|scp|rsync):*:hosts-ipaddr' ignored-patterns \
            '^<->.<->.<->.<->' '127.0.0.<->'
    zstyle ':completion:*:(ssh|scp|rsync):*:users' ignored-patterns \
            adm bin daemon halt lp named shutdown sync

    zstyle -e ':completion:*:(ssh|scp|ping|host|nmap|rsync):*' hosts 'reply=(
            ${=${${(f)"$(cat {/etc/ssh_,~/.ssh/known_}hosts(|2)(N) \
                            /dev/null)"}%%[#| ]*}//,/ }
            ${=${(f)"$(cat /etc/hosts(|)(N) <<(ypcat hosts 2>/dev/null))"}%%\#*}
            ${=${${${${(@M)${(f)"$(<~/.ssh/config)"}:#Host *}#Host }:#*\**}:#*\?*}}
            )'

    # kill
    zstyle ':completion:*:*:kill:*:processes' list-colors '=(#b) #([0-9]#)*=0=01;31'
    zstyle ':completion:*:*:kill:*' menu yes select
    zstyle ':completion:*:kill:*' force-list always
    zstyle ':completion:*:kill:*' command 'ps -u $USER -o pid,%cpu,tty,cputime,cmd'
    zstyle ':completion:*:kill:*' insert-ids single
    zstyle ':completion:*:*:kill:*' menu yes select
    zstyle ':completion:*:kill:*' force-list always
    zstyle ':completion:*:processes' command 'ps -u $USER -o pid,%cpu,tty,cputime,cmd'
    #
    # Prevent CVS/SVN files/directories from being completed
    zstyle ':completion:*:(all-|)files' ignored-patterns '(|*/)CVS'
    zstyle ':completion:*:cd:*' ignored-patterns '(*/)#CVS'

    # Prevent lost+found directory from being completed
    zstyle ':completion:*:cd:*' ignored-patterns '(*/)#lost+found'

    # ignore completion functions for commands you don't have
    zstyle ':completion:*:functions' ignored-patterns '(_*|pre(cmd|exec))'

    # Ignore same file on rm
    zstyle ':completion:*:(rm|kill|diff):*' ignore-line yes
    zstyle ':completion:*:rm:*' file-patterns '*:all-files'

    # Ignore all for mcd
    zstyle ':completion:*:mcd:*' ignored-patterns '*'

    # man
    zstyle ':completion:*:man:*' separate-sections true

    # add gnu default completions
    compdef _gnu_generic ctags

    # automagic url quoter
    autoload -U url-quote-magic
    zle -N self-insert url-quote-magic

    # pip zsh completion start
    function _pip_completion {
      local words cword
      read -Ac words
      read -cn cword
      reply=( $( COMP_WORDS="$words[*]" \
                 COMP_CWORD=$(( cword-1 )) \
                 PIP_AUTO_COMPLETE=1 $words[1] ) )
    }

    compctl -K _pip_completion pip
    # pip zsh completion end

## Language<a id="orgheadline9"></a>

    export LANG=en_US.UTF-8
    export LC_ALL=en_US.UTF-8

## Terminal Color<a id="orgheadline10"></a>

    export TERM="xterm-256color"

## GTAGS<a id="orgheadline11"></a>

    export GTAGSCONF=$HOME/.globalrc

## Aliases<a id="orgheadline12"></a>

    alias ec="emacsclient"
    alias enw="emacs -nw"
    alias lot="lsof -n -i4TCP:"
    alias lou="lsof -n -i4UDP:"
    alias be="bundle exec"
    alias ber="bundle exec rake"

    alias for_tfa="DEPLOYMENT_CLIENT=tfa"
    alias for_mbfs="DEPLOYMENT_CLIENT=mbfs"
    alias for_nfsnz="DEPLOYMENT_CLIENT=nfsnz"
    alias ss_for_tfa="DEPLOYMENT_CLIENT=tfa foreman start"
    alias ss_for_nfsnz="DEPLOYMENT_CLIENT=nfsnz foreman start"
    alias ss_for_mbfsau="DEPLOYMENT_CLIENT=mbfsau foreman start"
    alias rc_for_tfa="DEPLOYMENT_CLIENT=tfa rails c"
    alias rc_for_nfsnz="DEPLOYMENT_CLIENT=nfsnz rails c"
    alias rc_for_mbfsau="DEPLOYMENT_CLIENT=mbfsau rails c"
    alias rs_for_tfa="DEPLOYMENT_CLIENT=tfa rails s"
    alias rs_for_nfsnz="DEPLOYMENT_CLIENT=nfsnz rails s"
    alias rs_for_mbfsau="DEPLOYMENT_CLIENT=mbfsau rails s"
    alias ss="foreman start"

    alias tmks="tmux kill-server"
    alias tmls="tmux list-sessions"
    alias tma="tmux a -t "
    alias tmn="tmux new -s "
    alias tmn-dev-server="ssh danielc@dev-server -t tmux new -s "
    alias tma-dev-server="ssh danielc@dev-server -t tmux a -t "
    alias tmls-dev-server="ssh danielc@dev-server -t tmux list-sessions"

    alias srcz="source ~/.zshrc"

## Custom Functions<a id="orgheadline13"></a>

    function kill_ps_with_port () {
        if [ "$#" -eq  "0" ]
        then
            echo "No arugments supplied"
        else
            lsof -n -i4TCP:$1 | grep LISTEN | awk '{ print $2 }' | head -1 |xargs kill
        fi
    }

    function define_alias_for_client () {
      alias for_tfa="DEPLOYMENT_CLIENT=tfa"
      alias as_nfsnz="echo 'DEPLOYMENT_CLIENT=nfsnz' > .env"
      alias ss_for_tfa="DEPLOYMENT_CLIENT=tfa foreman start"
      alias rc_for_tfa="DEPLOYMENT_CLIENT=tfa rails c"
    }
