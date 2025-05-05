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
%{buildroot} = %{_buildrootdir}/%{name}-%{version}-%{release}.%{_arch} same as $BUILDROOT
%{_topdir} = %{getenv:HOME}/rpmbuild
%{_builddir} = %{_topdir}/BUILD
%{_rpmdir} = %{_topdir}/RPMS
%{_sourcedir} = %{_topdir}/SOURCES
%{_specdir} = %{_topdir}/SPECS
%{_srcrpmdir} =%{_topdir}/SRPMS
%{_buildrootdir} = %{_topdir}/BUILDROOT

Finding BuildRequires Entries:
Devel packages contain a pkgconfig folder with a file inside that can be called upon using pkgconfig()
This can also be done if the devel package contains a cmake folder. In cmake case you can call cmake()
typlib, %{mklibname "packagename"} can be used to called library packages if there is no other ways to do so.


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

NodeJS:
npm pack in extracted tar will create archive with dependencies.
%nodejs_install = install macro same as doing npm_config_prefix=%{buildroot}%{_prefix} npm install -g %{S:0}


Pnpm:
pnpm config set store-dir pnpm_store = store dependencies to pnpm_store folder
pnpm install --frozen = will download dependencies to the folder above folder
pnpm config set store-dir %{_builddir}/%{name}-%{version}/pnpm_store = will set extracted pnpm_store folder as dependencies folder

%build
pnpm config set store-dir %{builddir}/%{name}-%{version}
pnpm install --offline --frozen --force
pnpm build(?) options in package.json file


Electron:
ELECTRON_CACHE=  allows to pick local directory to download needed archive
