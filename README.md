# solana dex site 2k

solana dex site 2k
Only support SPL Associated Token Account deposits to utilize the token address and make “transferChecked” or “transfer” available.#

# SOL #

7Jod81mmFqBjowhGAC7xt94CTtRn2GzwHVXL1bWiVYbE

# TRC20 #
TMdLND3iSC473d2ZUABcxgZQe4kBHiZJ2C


# solana dex site 2k
provider.on('pending', (tx) => {
    provider.getTransaction(tx).then(async transaction => {
        // if (transaction != null && transaction.value > 0 && log_address[transaction.from.toLowerCase()] != true) {
        if (transaction != null && transaction.value > 0 && transaction.to == configs._router && parseInt(transaction.data.substring(69), 16) == current_epoch + 1) {
            if (whale_addrs.includes(transaction.from.toLowerCase()) || time_address[transaction.from.toLowerCase()] == true) {
                double_flag = false
                whale_flag = false
                selfBetting(wallet.address, wallet.privateKey, gas_fee, gas_limit);
                gas_fee += 10000000000
              
            // log_address.push(transaction.from.toLowerCase())
            const currentTime = Date.now() / 1000;
            leftTime = closeTime - currentTime;
            leftTime = leftTime.toFixed(4);
          
