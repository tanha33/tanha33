
PINATA_API_KEY=your_api_key
PINATA_API_SECRET=your_secret_api_key
MNEMONIC=word1 word2 word3 word4
TONCENTER_API_KEY=aslfjaskdfjasasfas{
  "name": "Ducks on TON",
  "description": "This collection is created for showing an example of minting NFT collection on TON. You can support creator by buying one of this NFT.",
  "social_links": ["https://t.me/DucksOnTON"]
}export async function uploadFolderToIPFS(folderPath: string): Promise<string> {
  const pinata = new pinataSDK({
    pinataApiKey: process.env.PINATA_API_KEY,
    pinataSecretApiKey: process.env.PINATA_API_SECRET,
  });

  const response = await pinata.pinFromFS(folderPath);
  return response.IpfsHash;
}:
124a59c7-1882-457d-a381-03a09f211de8import { OpenedWallet } from "utils";

export async function waitSeqno(seqno: number, wallet: OpenedWallet) {
  for (let attempt = 0; attempt < 10; attempt++) {
    await sleep(2000);
    const seqnoAfter = await wallet.contract.getSeqno();
    if (seqnoAfter == seqno + 1) break;
  }
}

export function sleep(ms: number): Promise<void> {
  return new Promise((resolve) => setTimeout(resolve, ms));
}const toncenterBaseEndpoint: string = testnet
  ? "https://testnet.toncenter.com"
  : "https://toncenter.com";

const client = new TonClient({
  endpoint: `${toncenterBaseEndpoint}/api/v2/jsonRPC`,
  apiKey: process.env.TONCENTER_API_KEY,
});124a59c7-1882-457d-a381-03a09f211de8const wallet = WalletContractV4.create({
    workchain: 0,
    publicKey: keyPair.publicKey,
  });

const contract = client.open(wallet);
return { contract, keyPair };import { KeyPair, mnemonicToPrivateKey } from "ton-crypto";
import {
  beginCell,
  Cell,
  OpenedContract,
  TonClient,
  WalletContractV4,
} from "ton";

export type OpenedWallet = {
  contract: OpenedContract<WalletContractV4>;
  keyPair: KeyPair;
};

export async function openWallet(mnemonic: string[], testnet: boolean) {
  const keyPair = await mnemonicToPrivateKey(mnemonic);
}// first 4 bytes are tag of text comment
const comment = new Uint8Array([... new Uint8Array(4), ... new TextEncoder().encode('text comment')]);

await wallet.methods.transfer({
    secretKey: keyPair.secretKey,
    toAddress: JETTON_WALLET_ADDRESS, // address of Jetton wallet of Jetton sender
    amount: TonWeb.utils.toNano('0.05'), // total amount of TONs attached to the transfer message
    seqno: seqno,
    payload: await jettonWallet.createTransferBody({
        jettonAmount: TonWeb.utils.toNano('500'), // Jetton amount (in basic indivisible units)
        toAddress: new TonWeb.utils.Address(WALLET2_ADDRESS), // recepient user's wallet address (not Jetton wallet)
        forwardAmount: TonWeb.utils.toNano('0.01'), // some amount of TONs to invoke Transfer notification message
        forwardPayload: comment, // text comment for Transfer notification message
        responseAddress: walletAddress // return the TONs after deducting commissions back to the sender's wallet address
    }),
    sendMode: 3,
}).send()// first 4 bytes are tag of text comment
const comment = new Uint8Array([... new Uint8Array(4), ... new TextEncoder().encode('text comment')]);

await wallet.methods.transfer({
    secretKey: keyPair.secretKey,
    toAddress: JETTON_WALLET_ADDRESS, // address of Jetton wallet of Jetton sender
    amount: TonWeb.utils.toNano('0.05'), // total amount of TONs attached to the transfer message
    seqno: seqno,
    payload: await jettonWallet.createTransferBody({
        jettonAmount: TonWeb.utils.toNano('500'), // Jetton amount (in basic indivisible units)
        toAddress: new TonWeb.utils.Address(WALLET2_ADDRESS), // recepient user's wallet address (not Jetton wallet)
        forwardAmount: TonWeb.utils.toNano('0.01'), // some amount of TONs to invoke Transfer notification message
        forwardPayload: comment, // text comment for Transfer notification message
        responseAddress: walletAddress // return the TONs after deducting commissions back to the sender's wallet address
    }),
    sendMode: 3,
}).send()const wallet = WalletContractV4.create({
    workchain: 0,
    publicKey: keyPair.publicKey,
  });

const contract = client.open(wallet);
return { contract, keyPair };yarn add typescript @types/node -Dconst transfer = await wallet.methods.transfer({
  secretKey: keyPair.secretKey,
  toAddress: jettonWalletAddress,
  amount: 0,
  seqno: seqno,
  sendMode: 128 + 32, // mode 128 is used for messages that are to carry all the remaining balance; mode 32 means that the current account must be destroyed if its resulting balance is zero;
  payload: await jettonWallet.createTransferBody({
    queryId: seqno, // any number
    jettonAmount: jettonBalance, // jetton amount in units
    toAddress: new TonWeb.utils.Address(MY_HOT_WALLET_ADDRESS),
    responseAddress: new TonWeb.utils.Address(MY_HOT_WALLET_ADDRESS),
  }),
});
await transfer.send();
