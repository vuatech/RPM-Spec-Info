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
