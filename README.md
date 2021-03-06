# NAME

Data::Object::Role::Formulatable - Objectify Class Attributes

# ABSTRACT

Formulatable Role for Perl 5

# SYNOPSIS

    package Test::Student;

    use registry;
    use routines;

    use Data::Object::Class;
    use Data::Object::ClassHas;

    with 'Data::Object::Role::Formulatable';

    has 'name';
    has 'dates';

    sub formulate {
      {
        name => 'test/data/str',
        dates => 'test/data/str'
      }
    }

    package main;

    my $student = Test::Student->new({
      name => 'levi nolan',
      dates => ['1587717124', '1587717169']
    });

    # $student->name;
    # <Test::Data::Str>

    # $student->dates;
    # [<Test::Data::Str>]

# DESCRIPTION

This package provides a mechanism for automatically inflating objects from
constructor arguments.

# INTEGRATES

This package integrates behaviors from:

[Data::Object::Role::Buildable](https://metacpan.org/pod/Data%3A%3AObject%3A%3ARole%3A%3ABuildable)

# LIBRARIES

This package uses type constraints from:

[Types::Standard](https://metacpan.org/pod/Types%3A%3AStandard)

# SCENARIOS

This package supports the following scenarios:

## automation

    package Test::Teacher;

    use registry;
    use routines;

    use Data::Object::Class;
    use Data::Object::ClassHas;

    with 'Data::Object::Role::Formulatable';

    has 'name';
    has 'dates';

    sub formulate {
      {
        name => 'test/data/str',
        dates => 'test/data/str'
      }
    }

    sub after_formulate {
      {
        name => 1
      }
    }

    sub after_formulate_name {
      my ($self, $value) = @_;

      $value
    }

    sub before_formulate {
      {
        name => 1
      }
    }

    sub before_formulate_name {
      my ($self, $value) = @_;

      $value
    }

    package main;

    my $teacher = Test::Teacher->new({
      name => 'levi nolan',
      dates => ['1587717124', '1587717169']
    });

    # $teacher->name;
    # <Test::Data::Str>

    # $teacher->dates;
    # [<Test::Data::Str>]

This package supports automatically calling _"before"_ and _"after"_ routines
specific to each piece of data provided. This is automatically enabled if the
presence of a `before_formulate` and/or `after_formulate` routine is
detected. If so, these routines should return a hashref keyed off the class
attributes where the values are either `1` (denoting that the hook name should
be generated) or some other routine name.

# AUTHOR

Al Newkirk, `awncorp@cpan.org`

# LICENSE

Copyright (C) 2011-2019, Al Newkirk, et al.

This is free software; you can redistribute it and/or modify it under the terms
of the The Apache License, Version 2.0, as elucidated in the ["license
file"](https://github.com/iamalnewkirk/data-object-role-formulatable/blob/master/LICENSE).

# PROJECT

[Wiki](https://github.com/iamalnewkirk/data-object-role-formulatable/wiki)

[Project](https://github.com/iamalnewkirk/data-object-role-formulatable)

[Initiatives](https://github.com/iamalnewkirk/data-object-role-formulatable/projects)

[Milestones](https://github.com/iamalnewkirk/data-object-role-formulatable/milestones)

[Contributing](https://github.com/iamalnewkirk/data-object-role-formulatable/blob/master/CONTRIBUTE.md)

[Issues](https://github.com/iamalnewkirk/data-object-role-formulatable/issues)
