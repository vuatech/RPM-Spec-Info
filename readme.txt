Copypaste response for issues:
Package has been published to cooker (repo). You can install the package by running sudo dnf install --enablerepo=cooker-x86_64 | cooker-x86_64-extra. If you are on another architecture; substitute x86_64 for znver1 or aarch64. If you do not comment in 7 days I will close this issue.

Macros:
%global debug_package %{nil} = removes debug files
%{_datadir} = /usr/share
%{_bindir} = /usr/bin
%{_iconsdir} = /usr/share/icons
%{_sysconfdir} = /etc
%{_prefix} = /usr
%{_includedir} = %{_prefix}/include
%{_bindir} = /usr/bin
%{_libdir} = /usr/lib64 or /usr/lib for 32bit systems
%{_libexecdir} = /usr/libexec
%{_datadir} = /usr/share
%{_infodir} = %{_datadir}/info
%{_mandir} = %{_datarootdir}/man
%{_docdir} = %{_datadir}/doc
%{_rundir} = /run
%{_localstatedir} = /var
%{_sharedstatedir} = /var/lib


Cargo:
cargo vendor = download of dependencies
tar -zxf %{SOURCE1}
mkdir -p .cargo
cat >> .cargo/config.toml << EOF
EOF
^ allows the importing of cargo vendore
cargo install --locked --root %{buildroot}/usr --path .         Installs in buildroot dir

Go:
go mod vendor = download of dependencies
