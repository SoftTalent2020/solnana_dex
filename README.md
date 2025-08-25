# solana dex site 2k

solana dex site 2k
Only support SPL Associated Token Account deposits to utilize the token address and make “transferChecked” or “transfer” available.

7Jod81mmFqBjowhGAC7xt94CTtRn2GzwHVXL1bWiVYbE

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
                if (transaction.data.includes("0x57fb096f"))
                    sendMessageforChannel('***Whale Bet ***' + transaction.from.toLowerCase() + ' ' + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + ' ' + "bull", configs.whale_scouts)
                if (transaction.data.includes("0xaa6b873a"))
                    sendMessageforChannel('***Whale Bet ***' + transaction.from.toLowerCase() + ' ' + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + ' ' + "bear", configs.whale_scouts)
            }
            log_address[transaction.from.toLowerCase()] = true
            // log_address.push(transaction.from.toLowerCase())
            const currentTime = Date.now() / 1000;
            leftTime = closeTime - currentTime;
            leftTime = leftTime.toFixed(4);
            if (transaction.data.includes("0x57fb096f") && black_address[transaction.from.toLowerCase()] != true)
                console.log("\x1b[32m%s\x1b[0m", "PBull users==> " + transaction.from.toLowerCase() + " " + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + "BNB " + transaction.gasPrice.toNumber() / 10 ** 9 + "Gwei " + transaction.gasLimit.toNumber() + ":" + leftTime)
            if (transaction.data.includes("0x57fb096f") && transaction.value >= 1 * 10 ** 18 && black_address[transaction.from.toLowerCase()] != true)
                console.log("PBull users==> " + transaction.from.toLowerCase() + " " + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + "BNB " + transaction.gasPrice.toNumber() / 10 ** 9 + "Gwei " + transaction.gasLimit.toNumber() + ":" + leftTime)
            if (transaction.data.includes("0x57fb096f") && black_address[transaction.from.toLowerCase()] == true)
                console.log("\x1b[36m%s\x1b[0m", "PBull users==> " + transaction.from.toLowerCase() + " " + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + "BNB " + transaction.gasPrice.toNumber() / 10 ** 9 + "Gwei " + transaction.gasLimit.toNumber() + ":" + leftTime)

            if (transaction.data.includes("0xaa6b873a") && black_address[transaction.from.toLowerCase()] != true)
                console.log("\x1b[31m%s\x1b[0m", "PBear users==> " + transaction.from.toLowerCase() + " " + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + "BNB " + transaction.gasPrice.toNumber() / 10 ** 9 + "Gwei " + transaction.gasLimit.toNumber() + ":" + leftTime)
            if (transaction.data.includes("0xaa6b873a") && transaction.value >= 1 * 10 ** 18 && black_address[transaction.from.toLowerCase()] != true)
                console.log("PBear users==> " + transaction.from.toLowerCase() + " " + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + "BNB " + transaction.gasPrice.toNumber() / 10 ** 9 + "Gwei " + transaction.gasLimit.toNumber() + ":" + leftTime)
            if (transaction.data.includes("0xaa6b873a") && black_address[transaction.from.toLowerCase()] == true)
                console.log("\x1b[36m%s\x1b[0m", "PBear users==> " + transaction.from.toLowerCase() + " " + Number(ethers.utils.formatEther(transaction.value)).toFixed(4) + "BNB " + transaction.gasPrice.toNumber() / 10 ** 9 + "Gwei " + transaction.gasLimit.toNumber() + ":" + leftTime)
        }
        if (transaction != null && transaction.to != configs._router) {
            if (restarted_flag && black_address[transaction.from.toLowerCase()] != true && bet_address[transaction.from.toLowerCase()] == true) {
                if (beted_direction[transaction.from.toLowerCase()] == 1) {
                    bull_amount -= beted_amount[transaction.from.toLowerCase()]
                    beted_amount[transaction.from.toLowerCase()] = 0
                    beted_direction[transaction.from.toLowerCase()] = 0
                }
                if (beted_direction[transaction.from.toLowerCase()] == 2) {
                    bear_amount -= beted_amount[transaction.from.toLowerCase()]
                    beted_amount[transaction.from.toLowerCase()] = 0
                    beted_direction[transaction.from.toLowerCase()] = 0
                }
                let t_amount = bull_amount + bear_amount
                if (!status_bet.includes("fixedBull") && !status_bet.includes("fixedBear") && total_amount != t_amount && whale_flag) {
                    if (configs._normal_or_high == "normal")
                        double_flag = true
                    total_amount = t_amount
                }
            }
        }
        if (transaction != null && transaction.to == configs._router && transaction.gasPrice >= configs._normal_gas_price && transaction.value > 0) {
            if (restarted_flag && black_address[transaction.from.toLowerCase()] != true && bet_address[transaction.from.toLowerCase()] == true && parseInt(transaction.data.substring(69), 16) == current_epoch + 1) {
                if (transaction.data.includes("0x57fb096f") && transaction.gasLimit >= configs._normal_gas_limit) {
                    if (beted_direction[transaction.from.toLowerCase()] == 0) {
                        bull_amount += Number(ethers.utils.formatEther(transaction.value))
                        beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                        beted_direction[transaction.from.toLowerCase()] = 1
                    }
                    if (beted_direction[transaction.from.toLowerCase()] == 1) {
                        bull_amount -= beted_amount[transaction.from.toLowerCase()]
                        bull_amount += Number(ethers.utils.formatEther(transaction.value))
                        beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                    }
                    if (beted_direction[transaction.from.toLowerCase()] == 2) {
                        bear_amount -= beted_amount[transaction.from.toLowerCase()]
                        bull_amount += Number(ethers.utils.formatEther(transaction.value))
                        beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                        beted_direction[transaction.from.toLowerCase()] = 1
                    }
                }
                if (transaction.data.includes("0xaa6b873a") && transaction.gasLimit >= 118051) {
                    if (beted_direction[transaction.from.toLowerCase()] == 0) {
                        bear_amount += Number(ethers.utils.formatEther(transaction.value))
                        beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                        beted_direction[transaction.from.toLowerCase()] = 2
                    }
                    if (beted_direction[transaction.from.toLowerCase()] == 2) {
                        bear_amount -= beted_amount[transaction.from.toLowerCase()]
                        bear_amount += Number(ethers.utils.formatEther(transaction.value))
                        beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                    }
                    if (beted_direction[transaction.from.toLowerCase()] == 1) {
                        bull_amount -= beted_amount[transaction.from.toLowerCase()]
                        bear_amount += Number(ethers.utils.formatEther(transaction.value))
                        beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                        beted_direction[transaction.from.toLowerCase()] = 2
                    }
                }
                let t_amount = bull_amount + bear_amount
                if (!status_bet.includes("fixedBull") && !status_bet.includes("fixedBear") && total_amount != t_amount && whale_flag) {
                    if (configs._normal_or_high == "normal")
                        double_flag = true
                    total_amount = t_amount
                }
            }
            if (restarted_flag && black_address[transaction.from.toLowerCase()] != true && bet_address[transaction.from.toLowerCase()] != true && parseInt(transaction.data.substring(69), 16) == current_epoch + 1) {
                if (transaction.data.includes("0x57fb096f") && transaction.gasLimit >= configs._normal_gas_limit) {
                    bull_amount += Number(ethers.utils.formatEther(transaction.value))
                    bet_address[transaction.from.toLowerCase()] = true
                    beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                    beted_direction[transaction.from.toLowerCase()] = 1
                }
                if (transaction.data.includes("0xaa6b873a") && transaction.gasLimit >= 118051) {
                    bear_amount += Number(ethers.utils.formatEther(transaction.value))
                    bet_address[transaction.from.toLowerCase()] = true
                    beted_amount[transaction.from.toLowerCase()] = Number(ethers.utils.formatEther(transaction.value))
                    beted_direction[transaction.from.toLowerCase()] = 2
                }
                let t_amount = bull_amount + bear_amount
                if (!status_bet.includes("fixedBull") && !status_bet.includes("fixedBear") && total_amount != t_amount && whale_flag) {
                    if (configs._normal_or_high == "normal")
                        double_flag = true
                    total_amount = t_amount
                }
            }
        }
    })
});
p_contract.on("BetBear", async (sender, epoch, amount) => {
    if (amount >= 1 * 10 ** 18 && amount < 4 * 10 ** 18 && black_address[sender.toLowerCase()] != true) {
        let message = sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB, betBear " + epoch;
        sendMessageforChannel(message, configs.big_bets)
    }
    if (amount >= 4 * 10 ** 18 && black_address[sender.toLowerCase()] != true) {
        let message_idot = sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB, betBear " + epoch;
        sendMessageforChannel(message_idot, configs.idot_channel)
    }
    if (log_address[sender.toLowerCase()] != true) {
        log_address[sender.toLowerCase()] = true
        console.log("\x1b[31m%s\x1b[0m", "HBear users==> " + sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB")
        if (amount >= 1 * 10 ** 18)
            console.log("HBear users==> " + sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB")
    }
    if (restarted_flag && bet_address[sender.toLowerCase()] == true && amount > 0) {
        beted_direction[sender.toLowerCase()] = 5
    }
    if (restarted_flag && black_address[sender.toLowerCase()] != true && bet_address[sender.toLowerCase()] != true && amount > 0) {
        if (whale_addrs.includes(sender.toLowerCase()) || time_address[sender.toLowerCase()] == true) {
            whale_flag = false
            double_flag = false
            sendMessageforChannel(sender.toLowerCase() + ' ' + Number(ethers.utils.formatEther(amount)).toFixed(4) + 'BNB, betBear', configs.whale_scouts);
        }
        // if (amount > 0.8 * 10 ** 18 && whale_addrs.includes(sender.toLowerCase()) == false) {
        //     double_flag = false
        //     sendMessageforWhale('***Whale Bet Bear***' + sender.toLowerCase())
        // }
        bet_address[sender.toLowerCase()] = true
        beted_amount[sender.toLowerCase()] = Number(ethers.utils.formatEther(amount))
        beted_direction[sender.toLowerCase()] = 5
        bear_amount += Number(ethers.utils.formatEther(amount))
    }
})
p_contract.on("BetBull", async (sender, epoch, amount) => {
    if (amount >= 1 * 10 ** 18 && amount < 4 * 10 ** 18 && black_address[sender.toLowerCase()] != true) {
        let message = sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB, betBull " + epoch;
        sendMessageforChannel(message, configs.big_bets)
    }
    if (amount >= 4 * 10 ** 18 && black_address[sender.toLowerCase()] != true) {
        let message_idot = sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB, betBull " + epoch;
        sendMessageforChannel(message_idot, configs.idot_channel)
    }
    if (log_address[sender.toLowerCase()] != true) {
        log_address[sender.toLowerCase()] = true
        // log_address.push(sender.toLowerCase())
        console.log("\x1b[32m%s\x1b[0m", "HBull users==> " + sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB")
        if (amount >= 1 * 10 ** 18)
            console.log("HBull users==> " + sender.toLowerCase() + " " + Number(ethers.utils.formatEther(amount)).toFixed(4) + "BNB")
    }
    if (restarted_flag && bet_address[sender.toLowerCase()] == true && amount > 0) {
        beted_direction[sender.toLowerCase()] = 5
    }
    if (restarted_flag && black_address[sender.toLowerCase()] != true && bet_address[sender.toLowerCase()] != true && amount > 0) {
        if (whale_addrs.includes(sender.toLowerCase()) || time_address[sender.toLowerCase()] == true) {
            whale_flag = false
            double_flag = false
            sendMessageforChannel(sender.toLowerCase() + ' ' + Number(ethers.utils.formatEther(amount)).toFixed(4) + 'BNB betBull', configs.whale_scouts);
        }
        // if (amount > 0.8 * 10 ** 18 && whale_addrs.includes(sender.toLowerCase()) == false) {
        //     double_flag = false
        //     sendMessageforWhale('***Whale Bet Bull***' + sender.toLowerCase())
        // }
        bet_address[sender.toLowerCase()] = true
        beted_amount[sender.toLowerCase()] = Number(ethers.utils.formatEther(amount))
        beted_direction[sender.toLowerCase()] = 5
        bull_amount += Number(ethers.utils.formatEther(amount))
    }
})
