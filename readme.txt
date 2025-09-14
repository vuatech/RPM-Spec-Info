--Copypaste response for issues:
Package has been published to cooker (repo). You can install the package by running sudo dnf install --enablerepo=(cooker-x86_64, cooker-x86_64-non-free, cooker-x86_64-restricted, or cooker-x86_64-extra). If you are on another architecture; substitute x86_64 for znver1 or aarch64.

Macros:
%global debug_package %{nil} = removes debug files
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
%{_unitdir} = /usr/lib/systemd
%{_userunitdir} = /usr/lib/systemd/user
%{buildroot} = %{_buildrootdir}/%{name}-%{version}-%{release}.%{_arch} same as $BUILDROOT
%{_topdir} = %{getenv:HOME}/rpmbuild
%{_builddir} = %{_topdir}/BUILD
%{_rpmdir} = %{_topdir}/RPMS
%{_sourcedir} = %{_topdir}/SOURCES
%{_specdir} = %{_topdir}/SPECS
%{_srcrpmdir} =%{_topdir}/SRPMS
%{_buildrootdir} = %{_topdir}/BUILDROOT
%{py_sitedir} = %{_libdir}/python%{pyver}/site-packages/

%{_datadir}/bash-completions/completions/
%{_datadir}/fish-completions/completions/
%{_datadir}/zsh-completions/completions/

 %{pyver} = Used to call current version of python used by system. python%{pyver}dist(pygobject) will call python-gobject package.


Finding BuildRequires Entries:
Devel packages contain a pkgconfig folder with a file inside that can be called upon using pkgconfig()
This can also be done if the devel package contains a cmake folder. In cmake case you can call cmake()
typlib, %{mklibname "packagename"} can be used to called library packages if there is no other ways to do so.
Test logs/mock output from abf/build process can be used to frind provided lines for packages.

Cargo:
cargo vendor = download of dependencies into a vendor folder. This vendor folder needs to be compressed and added as a source
tar -zxf %{SOURCE1}
mkdir -p .cargo
cat >> .cargo/config.toml << EOF
{results from cargo vendor at the end of the process}
EOF
^ allows the importing of cargo dependencies

cargo build --frozen --release
install -dm0755 %{buildroot}%{_bindir}
install -Dm0755 target/release/%{name} %{buildroot}%{_bindir}

Go:
go mod vendor = download of dependencies in vendor folder. Needs to be compressed and added to source
install -dm0755 %{buildroot}%{_binddir}
go build -o %{buildroot}%{_bindir}

NodeJS:
npm install 'packagename'@'version' --omit=dev --cache ~/.npm   =  Will download cache and dependencies locally
export NPM_CONFIG_CACHE=$PWD/.npm  =  will extract npm cache to local build directory
%nodejs_install = install macro same as doing npm_config_prefix=%{buildroot}%{_prefix} npm install -g %{S:0}


Pnpm: (Work In Progress)
pnpm config set cache-dir cache = store cache to cache folder (might be uneccessary if pnpm_store work)
pnpm config set store-dir pnpm_store = store dependencies to pnpm_store folder (might be uneccessary if cache works)
pnpm install --frozen = will download dependencies to the folder above folder
pnpm config set store-dir %{_builddir}/%{name}-%{version}/pnpm_store = will set extracted pnpm_store folder as dependencies folder

%build
pnpm config set cache-dir %{_builddir}/%{name}-%{version}/cache (might be uneccessary if pnpm_store works)
pnpm config set store-dir %{builddir}/%{name}-%{version}/pnpm_store (might be uneccessary if cache works)
pnpm install --offline --frozen --force
pnpm build(?) options in package.json file


Electron:
ELECTRON_CACHE=  allows to pick local directory to download needed archive

git init
git add 
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/OpenMandrivaAssociation/*.git
git push -u origin master
