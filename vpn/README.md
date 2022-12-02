### Connecting to the VPN

Get Certs

```
aws ssm get-parameter --name "dev_vpn_key" --with-decryption \
        --output text --query Parameter.Value > key.txt

aws ssm get-parameter --name "dev_vpn_certificate" --with-decryption \
        --output text --query Parameter.Value > cert.txt

aws ec2 export-client-vpn-client-configuration \
        --client-vpn-endpoint-id cvpn-endpoint-0b1df2b162a5679e1 \
        --output text > vpn.txt
```

Connect

```
sudo openvpn --config vpn.txt \
        --key key.txt --cert cert.txt
```