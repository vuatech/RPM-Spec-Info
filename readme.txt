Copypaste response for issues:
Package has been published to cooker (repo). You can install the package by running sudo dnf install --enablerepo=cooker-x86_64 | cooker-x86_64-extra. If you are on another architecture; substitute x86_64 for znver1 or aarch64. If you do not comment in 7 days I will close this issue.

Macros:
%global debug_package %{nil} = removes debug files
%{_datadir} = /usr/share
%{_bindir} = /usr/bin
%{_iconsdir} = /usr/share/icons


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
