$script = <<SCRIPT

echo Enabling X11Forwarding
echo X11Forwarding yes >> /etc/ssh/sshd_config
echo Restarting sshd
/etc/rc.d/rc.sshd restart

echo Creating /usr/X11R6/lib/X11/locale/
mkdir -p /usr/X11R6/lib/X11
ln -s /usr/share/X11/locale /usr/X11R6/lib/X11/

echo Downloading libc5
curl -s http://slackware.cs.utah.edu/pub/slackware/slackware-7.1/slakware/a9/libc5.tgz | tar -C / -xzf -
echo Downloading libc5x
curl -s http://slackware.cs.utah.edu/pub/slackware/slackware-7.1/slakware/x1/libc5x.tgz | tar -C / -xzf -
echo /usr/i386-slackware-linux-gnulibc1/lib >> /etc/ld.so.conf
ln -s /usr/i386-slackware-linux-gnulibc1/lib/ld-linux.so.1.9.9 /lib/ld-linux.so.1
ldconfig

echo Downloading xplns
curl -s http://www.astroarts.com/products/xplns/binaries/xplns-3.3.1-1-linux.tar.gz | tar -xzf -
curl -s http://www.astroarts.com/products/xplns/binaries/xplns-cat-3.3.1-1-linux.tar.gz | tar -xzf -
curl -s http://www.astroarts.com/products/xplns/binaries/xplns-elm-3.3.1-1-linux.tar.gz | tar -xzf -
curl -s http://www.astroarts.com/products/xplns/binaries/xplns-img-3.3.1-1-linux.tar.gz | tar -xzf -

cd xplns-3.3.1
./install.sh -x

echo xplns ready to run:
echo vagrant ssh -c xplns

SCRIPT

Vagrant.configure(2) do |config|
  config.ssh.forward_x11 = true
  config.vm.box = "talosthoren/slackware-multilib"
  config.vm.provision "shell", inline: $script
end
