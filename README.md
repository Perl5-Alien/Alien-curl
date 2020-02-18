# Alien::curl [![Build Status](https://secure.travis-ci.org/plicease/Alien-curl.png)](http://travis-ci.org/plicease/Alien-curl)

Discover or download and install curl + libcurl

# SYNOPSIS

In your script or module:

```perl
use Alien::curl;
use Env qw( @PATH );

unshift @PATH, Alien::curl->bin_dir;
```

In your Build.PL:

```perl
use Module::Build;
use Alien::curl;
my $builder = Module::Build->new(
  ...
  configure_requires => {
    'Alien::curl' => '0',
    ...
  },
  extra_compiler_flags => Alien::curl->cflags,
  extra_linker_flags   => Alien::curl->libs,
  ...
);

$build->create_build_script;
```

In your Makefile.PL:

```perl
use ExtUtils::MakeMaker;
use Config;
use Alien::curl;

WriteMakefile(
  ...
  CONFIGURE_REQUIRES => {
    'Alien::curl' => '0',
  },
  CCFLAGS => Alien::curl->cflags . " $Config{ccflags}",
  LIBS    => [ Alien::curl->libs ],
  ...
);
```

In your [FFI::Platypus](https://metacpan.org/pod/FFI::Platypus) script or module:

```perl
use FFI::Platypus;
use Alien::curl;

my $ffi = FFI::Platypus->new(
  lib => [ Alien::curl->dynamic_libs ],
);
```

# DESCRIPTION

This distribution provides curl so that it can be used by other
Perl distributions that are on CPAN.  It does this by first trying to
detect an existing install of curl on your system.  If found it
will use that.  If it cannot be found, the source code will be downloaded
from the internet and it will be installed in a private share location
for the use of other modules.

# SEE ALSO

[Alien](https://metacpan.org/pod/Alien), [Alien::Base](https://metacpan.org/pod/Alien::Base), [Alien::Build::Manual::AlienUser](https://metacpan.org/pod/Alien::Build::Manual::AlienUser)

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2017 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
