# dpkg-query

Find installed package by name:

    dpkg-query -W | grep vim

Find installed package containing file:

    dpkg-query -S /usr/bin/vim.nox

List files installed by package:

    dpkg-query -L vim-nox
