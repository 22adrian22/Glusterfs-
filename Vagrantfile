Vagrant.configure("2") do |config|
  # Configuración del primer servidor GlusterFS
  config.vm.define "gluster1" do |gluster1|
    gluster1.vm.box = "debian/bookworm64"
    gluster1.vm.network "private_network", ip: "192.168.57.101"
  end

  # Configuración del segundo servidor GlusterFS
  config.vm.define "gluster2" do |gluster2|
    gluster2.vm.box = "debian/bookworm64"
    gluster2.vm.network "private_network", ip: "192.168.57.102"
  end

  # Configuración del cliente GlusterFS
  config.vm.define "client" do |client|
    client.vm.box = "debian/bookworm64"
    client.vm.network "private_network", ip: "192.168.57.103"
  end
end
