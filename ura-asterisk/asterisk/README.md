
gcloud compute ssh --project ancient-medium-466012-d9 asterisk-vm

gcloud compute scp --recurse ./asterisk/*.conf \
    asterisk-vm:/home/fernandopessoa/asterisk-config/

sudo systemctl start asterisk

sudo asterisk -f -rvvvvvvv